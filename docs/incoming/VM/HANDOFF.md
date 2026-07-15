# HANDOFF — Parallel Isolated Input Forwarding (bot-in-a-sandbox)

**Audience:** the next agent (or engineer) picking this up cold.
**Repo root:** `C:\UserProgram\MetaProgram` (repo-relative paths below are under this root)
**This package (docs) lives in:** `C:\UserProgram\MetaProgram\docs\incoming\VM\` — repo-relative: `docs/incoming/VM/`
**Repo branch:** `claude/virtual-desktop-input-forwarding-xmz6vf`
**Status:** design-only schematic complete + verified; **no implementation code yet**.
**Platform target:** Windows 11, C++ (host + in-sandbox companion).

> **All document/diagram references in this file are full absolute paths** under
> `C:\UserProgram\MetaProgram\docs\incoming\VM\`. Adjust the prefix if the
> repo is cloned elsewhere. Planned *implementation code* paths use `<CODE_ROOT>/`
> — a to-be-decided location that is **not** this docs folder (see
> `C:\UserProgram\MetaProgram\docs\incoming\VM\IMPLEMENTATION.md` §3).

Read this file top-to-bottom once, then start at [§7 Implementation roadmap](#7-implementation-roadmap).
Everything here is distilled from the design docs in this repo — trust those as
the source of truth and this as the executable summary.

---

## 1. Mission (what we are building)

An **AI agent on the user's main desktop** drives an interactive application
(reference target: **Minecraft**) that runs inside an **isolated sandbox** — a
separate Windows session ("virtual desktop"/VD) **or** a virtual machine (VM) —
purely through a **parallel, synthetic input channel**. Never the game's APIs,
mods, or process memory: **pixels in, synthetic input out.**

Two hard requirements govern every decision:

- **R1 — Isolation + parallelism.** The sandbox has its *own* input stream. The
  user keeps using the main desktop, **undisturbed**; the two input streams
  never collide, and both run concurrently.
- **R2 — Game-received input.** Injected input must reach the paths a game
  actually reads (Raw Input, DirectInput, `GetAsyncKeyState`) — **not** merely a
  window's message queue.

The system is a **closed control loop**:
`capture frame → tracker (pixels→state) → AI (state→action) → input channel → companion injects → game renders → capture …`

---

## 2. The one correction that reframed everything

An earlier pass proposed a **Win32 desktop object (`HDESK`, `CreateDesktopEx`)**
— a hidden desktop. **That is the wrong tool** and must not be resurrected:

1. **No parallelism.** One session has a single kernel **Raw Input Thread (RIT)**
   and, at any instant, exactly **one input desktop**. Hardware input and
   `SendInput` route only there; `SwitchDesktop` is a mutually-exclusive full
   switch. Two desktops cannot carry two live input streams — they collide. → R1 fails.
2. **Games read below the message queue.** A background desktop can only be fed
   by `PostMessage`, but games read Raw Input / DirectInput / `GetAsyncKeyState`,
   all **blind to posted messages**. → R2 fails.

The requirement is met **one level up**: a **separate interactive session** or a
**VM**. `HDESK` is retained only as a "why-not" reference at
`C:\UserProgram\MetaProgram\docs\incoming\VM\VIRTUAL-DESKTOP-INPUT-FORWARDING.md`.

---

## 3. Decided facts (do not re-litigate)

These were cross-checked against vendor docs and adversarially reviewed. Treat as settled.

### Input reachability — strict ranking (for driving a *foreground* game)
`PostMessage` (window messages) **<** in-session `SendInput` **<** real/virtual **HID** device.

| Method | Reaches Win32 msg queue | async key-state (`GetAsyncKeyState`) | Raw Input (`WM_INPUT`) | DirectInput (excl.) |
|---|---|---|---|---|
| `PostMessage(WM_*)` | one window only | ✗ | ✗ | ✗ |
| in-session `SendInput` | ✓ | ✓ | ✓ but **flagged** `hDevice==NULL`, `LLKHF_INJECTED`, unreliable relative deltas | ✗ |
| real / **virtual HID** device | ✓ | ✓ | ✓ (genuine) | ✓ |

- `SendInput` **does** update Raw Input, but injected events are detectable
  (`hDevice==NULL`, `GetCurrentInputMessageSource()==IMO_INJECTED`) and it does
  **not** correctly produce **relative mouse deltas** for raw look-motion.
- **DirectInput is not the bypass**: modern DI keyboard/mouse rides on Raw Input,
  so it *does* see in-session `SendInput`. `PostMessage` is ineffective against
  DI at **all** cooperative levels. The real upstream bypass is a kernel/HID read.
- `GetKeyState` (per-queue, message-synced) and `GetAsyncKeyState` (global,
  near-real-time) are **distinct tables**; `SendInput` moves both, `PostMessage` neither.
- `SendInput` is scoped to the caller's session/desktop and UIPI — it **cannot
  cross** a session, a desktop object, or a VM guest. **The injector must live
  inside the sandbox.**

### Minecraft specifics (reference target)
- Java Edition = LWJGL3 + GLFW. Keyboard, menus, cursor-visible mouse → driven
  fine by in-session `SendInput`.
- **In-game look-motion** depends on the **"Raw Input"** video option:
  - Raw Input **OFF** → GLFW uses cursor-warp + `WM_MOUSEMOVE` → `SendInput`
    relative motion works.
  - Raw Input **ON (default where supported)** → look arrives via `WM_INPUT`
    relative deltas that `SendInput` cannot correctly produce → **virtual/kernel
    HID required.**
- Bedrock Edition uses a GameInput/gamepad stack → needs a **virtual controller**
  (ViGEmBus-style), not `SendInput`.

### Sandbox mechanism ranking
| Mechanism | R1 parallel | R1 isolation | R2 game-reach | Cost |
|---|---|---|---|---|
| HDESK desktop object | ✗ | ✗ | ✗ | — **rejected** |
| Separate session (VD) | ✓ own RIT/queue | ⚠ shared kernel/FS | in-session `SendInput` (+virtual HID for raw look) | ⚠ client single-console limit; disconnected-session lock/render issues |
| **Virtual machine (VM)** | ✓ separate stack | ✓ strongest | ✓ device-level HID reaches even exclusive DI | ⚠ guest OS + GPU + capture latency |
| Virtual HID driver | ✓ | (pairs with VD/VM) | ✓ device-level | ⚠ signed kernel driver |

---

## 4. Architecture (the split)

```
  HOST (user's main desktop, undisturbed)          SANDBOX (VM guest or separate session)
  ┌───────────────────────────────┐                ┌───────────────────────────────┐
  │  AI system   (policy → action)│  ── input ──▶  │  Process companion (injector) │
  │        ▲                      │   channel      │        │                      │
  │        │ state                │                │        ▼ virtual input        │
  │  Process tracker (capture)    │  ◀─ observation│  Target app (e.g. Minecraft)  │
  │  pixels → state, NO app API   │    channel     │  reads its own input stream   │
  └───────────────────────────────┘                └───────────────────────────────┘
                     └────────── closed loop, no in-band ACK ──────────┘
```

- **Host:** `process tracker` (frame capture + pixels→state, no app API) and
  `AI system` (state→action).
- **Sandbox:** `target app` and `process companion` (the injector).
- **Two channels:** observation (sandbox frames → host tracker) and input
  (host AI → sandbox companion → injected input).
- The full-resolution diagram set is in `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\` (see §9).

---

## 5. Recommended default path (start here, note the alternative)

**Default: VM + in-guest companion.**

- **Hypervisor:** VirtualBox (scriptable, free, `IKeyboard`/`IMouse` COM +
  `VBoxManage`) or Hyper-V. *(Decision open — see §6.)*
- **Injection:** an **in-guest companion** process that receives actions over a
  VM-native channel and injects locally via `SendInput` for keyboard/menu, and a
  **guest virtual HID** (relative mouse) for look-motion. Host-side hypervisor
  input APIs are the fallback (coarser, higher latency, weak on relative mouse).
- **Observation:** in-guest capturer (WGC of the game window) streaming frames to
  the host over the same VM channel; **or** host-side WGC capture of the live VM
  window. (Hyper-V has **no** low-latency host framebuffer API — don't build on
  the WMI thumbnail.)
- **Channel:** VM-native, no open port — Hyper-V sockets (`AF_HYPERV` /
  `AF_VSOCK`) or VMware VMCI/vSockets, or a shared-memory ring; host-only TCP is
  the last-resort fallback.

**Why default to VM:** cleanest R1 (separate device stack, zero input cross-talk),
reaches exclusive DirectInput, and avoids the client-SKU single-session / RDP
lock mess of the VD path.

**Alternative — separate session (VD):** lighter, lower capture latency (shared
GPU), but bounded by Windows client one-active-session limit (a 2nd concurrent
session needs unsupported RDPWrap/`termsrv.dll` patching — **do not ship on
that**), and a disconnected RDP session locks + stops rendering (black capture)
unless mitigated (`tscon` console redirect, disabled lock/timeout GPOs, a virtual
display via IddCx/dummy-plug, "use hardware graphics adapters for RDS sessions").

---

## 6. Open decisions (make these first, record the choice)

| # | Decision | Options | Recommendation |
|---|---|---|---|
| D1 | Isolation boundary | VM vs separate session (VD) | **VM** (isolation + game-reach); VD only if isolation is non-critical and latency is king |
| D2 | Hypervisor (if VM) | VirtualBox / Hyper-V / VMware | **VirtualBox** first (scriptable COM API, free, good docs) — revisit if GPU accel is needed |
| D3 | Mouse-look injection | in-guest `SendInput` / **guest virtual HID** / hypervisor rel-mouse | **guest virtual HID (relative)** — required for Minecraft Raw-Input-ON |
| D4 | Capture path | in-guest WGC stream / host-side WGC of VM window / GPU passthrough | **in-guest WGC** stream over VM channel (crop the game window in-guest) |
| D5 | Transport | vsock/Hyper-V sockets / VMCI / shared-mem / TCP | VM-native (**vsock/Hyper-V sockets**); TCP only as fallback |
| D6 | Policy | scripted (bring-up) → learned CNN → VLM | scripted for bring-up; small **CNN** for real-time; VLM only with frame-skip |
| D7 | Guest OS | Windows 11 (run Java MC) | Windows 11 guest |

---

## 7. Implementation roadmap

Each phase has an **acceptance test** — do not advance until it passes. Build a
tiny **input-probe** utility early (a guest app that prints `WM_INPUT` +
`GetAsyncKeyState` + message-queue events) — it is your ground truth for R2.

### Phase 0 — Scaffolding
- Repo layout: `host/` (tracker + AI + channel client), `guest/` (companion +
  capturer + channel server), `common/` (wire protocol, shared structs).
- Stand up the VM (D1/D2/D7); install the guest OS; get a build toolchain both sides.
- **Accept:** VM boots; you can build+run a hello-world on host and in guest.

### Phase 1 — Input channel + keyboard proof-of-life
- Implement the transport (D5) and a minimal wire protocol (key/mouse action records).
- In-guest companion receives a keypress action and injects via `SendInput`.
- **Accept:** host sends "press A"; the **input-probe in the guest** shows the
  keydown/keyup AND `GetAsyncKeyState` reflects it. Then: Notepad in the guest
  types "A". Then: Minecraft main-menu / chat receives keystrokes.

### Phase 2 — Mouse-look (the hard part)
- Add a **guest virtual relative-mouse HID** (D3). Inject relative dx/dy.
- **Accept:** with Minecraft **Raw Input ON**, the camera pans smoothly and
  proportionally; the input-probe shows genuine `WM_INPUT` relative deltas with a
  non-null `hDevice`. (If you only see look with Raw Input OFF, you're still on
  `SendInput` — not done.)

### Phase 3 — Observation channel
- In-guest capturer (D4): WGC of the game window → frames → host tracker.
- Handle DPI/resolution: pin guest resolution, disable DPI scaling, calibrate the
  screen→client coordinate transform once.
- **Accept:** host receives a live frame stream of the game at a stable rate;
  measure end-to-end **capture→host latency** (target: readback+transfer, not
  on-GPU capture, dominates — log it).

### Phase 4 — Close the loop (scripted policy)
- Wire capture → trivial scripted "policy" (e.g., walk forward 2s, look left,
  jump) → action → companion → game.
- **Accept:** a scripted behavior visibly executes in the game **while the user
  types normally on the host** (prove R1: host input is untouched).

### Phase 5 — Real policy
- Replace the scripted stub with a learned policy (D6). Add **frame-stacking or a
  recurrent model** (a single frame lacks velocity).
- Model the loop delay: **action-repeat / latency-aware** control (there is no
  in-band ACK; the action lands *k* frames late — see §8).
- **Accept:** the policy sustains its action rate within the frame budget
  (~16.7 ms/action @ 60 fps; small CNN fits, large VLM forces frame-skip).

### Phase 6 — Robustness / fail-safes
- **Foreground watchdog:** assert the game is the sandbox-foreground window every
  tick (silent focus loss = open-loop blind injection).
- **Key-release fail-safe:** on any loop stall with keys held, release all keys.
- **Frame de-dup + event-driven pacing:** WGC `FrameArrived` fires per DWM
  composition and re-delivers unchanged frames; dedupe.
- Reconnect logic for the channel; clean teardown.
- **Accept:** kill/restart each component; the system recovers or fails safe
  (no stuck keys, no runaway).

---

## 8. Gotchas / verified pitfalls (each has bitten someone)

- **Delivery ≠ acceptance.** `SendInput` is flagged injected; raw-input consumers
  can reject it, and it can't do raw relative mouselook → **virtual HID** (Phase 2).
- **Absolute vs relative mouse.** Absolute-coordinate virtual mice break relative
  FPS mouselook. Use a **relative-capable** device/path.
- **Off-by-k staleness.** One-way loop, no ACK; the only feedback is the next
  frame. Action lands *k* frames later, stale by (capture+inference+injection)
  latency. Model it; don't assume synchronous Gym `step()` semantics.
- **Capture latency is GPU→CPU readback + transfer**, not on-GPU capture. Use
  double-buffered/async readback; prefer shared-memory zero-copy or a lossless
  path (H.264/NVENC artifacts corrupt template-matching/OCR).
- **Capture is isolation-bound.** DXGI Desktop Duplication is session-scoped
  (can't reach across from host), needs an active/connected desktop, caps ~4
  concurrent, captures a *monitor* not a window. WGC captures a window (occluded
  OK, **minimized NOT**, exclusive-fullscreen bypasses DWM → run **borderless
  windowed**). GDI `BitBlt`/`PrintWindow` returns black on GPU content.
- **DPI / coordinate mismatch** mislocates every click. Pin resolution, disable
  DPI scaling, calibrate once; absolute mouse is primary-monitor-normalized
  0–65535 without `MOUSEEVENTF_VIRTUALDESK`.
- **Scancode injection is layout/NumLock-sensitive.** Use extended (`e0`) codes
  to disambiguate keypad vs navigation.
- **VirtualBox has no `VBoxManage` mouse CLI** — mouse goes through the `IMouse`
  COM API (`putMouseEvent` / `putMouseEventAbsolute`); keyboard has
  `keyboardputscancode`.
- **Separate-session traps:** client single-console limit; disconnected RDP
  locks + stops GPU render (black frames); needs `tscon` + virtual display + RDS
  GPU policy. RDPWrap/`termsrv.dll` patching is unsupported + update-fragile.
- **Foreground still matters inside the sandbox** even with device-level
  injection (it removes *host* focus sensitivity, not *guest*).

---

## 9. Repo map & references

**Design docs (source of truth):**
- `C:\UserProgram\MetaProgram\docs\incoming\VM\PARALLEL-INPUT-FORWARDING.md` — **the corrected design** (read first).
- `C:\UserProgram\MetaProgram\docs\incoming\VM\PARALLEL-INPUT-FORWARDING.html` — self-contained visual companion (same content + diagrams).
- `C:\UserProgram\MetaProgram\docs\incoming\VM\VIRTUAL-DESKTOP-INPUT-FORWARDING.md` — the HDESK "why-not" reference (superseded framing; still accurate about desktop objects).
- `C:\UserProgram\MetaProgram\docs\incoming\VM\VIRTUAL-DESKTOP-INPUT-FORWARDING.html` — visual companion for the HDESK reference.
- `C:\UserProgram\MetaProgram\docs\incoming\VM\HANDOFF.md` — this file.
- `C:\UserProgram\MetaProgram\docs\incoming\VM\IMPLEMENTATION.md` — the live implementation log / decision record (start here to record progress).
- `C:\UserProgram\MetaProgram\SCHEMATIC.md` — **unrelated** (an iLOQ/TypeScript schematic; ignore for this task).

**Diagrams (hand-authored SVG):**
- Corrected design:
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\architecture.svg`
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\mechanisms.svg`
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\reachability.svg`
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\loop.svg`
- HDESK reference:
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\taxonomy.svg`
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\topology.svg`
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\input-desktop.svg`
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\injection-modes.svg`
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\sequence.svg`
  - `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\lifecycle.svg`

**Key APIs / tooling to look up (Microsoft Learn + vendor docs):**
- Input read/inject: `RegisterRawInputDevices` / `WM_INPUT`, `GetRawInputData`,
  `SendInput`, `GetAsyncKeyState` vs `GetKeyState`, `GetCurrentInputMessageSource`.
- Virtual HID: ViGEmBus (gamepad), custom HID minidriver (kbd/mouse), Windows HID.
- Capture: Windows.Graphics.Capture (WGC), DXGI Desktop Duplication (DDA).
- VirtualBox: `IKeyboard`/`IMouse`/`IFramebuffer` COM, `VBoxManage controlvm ... keyboardputscancode`.
- Hyper-V: integration/sockets (`AF_HYPERV`, `HV_PROTOCOL_RAW`), guest `AF_VSOCK`.
- Sessions/display: `WTSQueryUserToken`, `CreateProcessAsUser`, `tscon`, IddCx virtual display.
- Prior art (validates the *policy*, not the OS injection layer): OpenAI VPT / MineRL.

---

## 10. Constraints & non-goals (keep the scope honest)

- **No application APIs, mods, plugins, or process-memory** — observation is
  pixels-only, input is synthetic-only.
- **No host-side injection across the isolation boundary** — `SendInput` can't
  cross a session/desktop/VM; the injector lives **inside** the sandbox.
- **Not** HDESK / Task View "virtual desktops" as the isolation mechanism.
- **Scope: local / single-player / self-hosted RL.** Synthetic input is flagged
  and virtual-HID/VM artifacts are fingerprintable; automating an **online** title
  may breach its ToS and trip kernel anti-cheat (which can enforce locally at
  boot). This is a transparency caveat — **no anti-cheat evasion is in scope**,
  and the design does not try to defeat it.
- Everything so far is **design-only**; there is no code to extend yet — you are
  starting implementation from the schematic.

---

## 11. First action for the receiving agent

1. Read `C:\UserProgram\MetaProgram\docs\incoming\VM\PARALLEL-INPUT-FORWARDING.md` and skim the four
   corrected diagrams in `C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\`.
2. Record decisions D1–D7 (§6) in `C:\UserProgram\MetaProgram\docs\incoming\VM\IMPLEMENTATION.md` (skeleton
   already committed — fill in the choices).
3. Do **Phase 0 + Phase 1** (§7) — get one synthetic keystroke to register in the
   guest's input-probe and in Minecraft. That single result de-risks the whole
   R2 question. Then proceed phase by phase, keeping each acceptance test green.
