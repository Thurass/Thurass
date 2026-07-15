# IMPLEMENTATION — Parallel Isolated Input Forwarding

**Live implementation log + decision record.** Update this file as you work.
**Repo root:** `/home/user/Thurass`
**This file lives in:** `/home/user/Thurass/metaprogram/docs/incoming/VM/IMPLEMENTATION.md`
**Branch:** `claude/virtual-desktop-input-forwarding-xmz6vf`

Design source of truth (read before touching this file):
- `/home/user/Thurass/metaprogram/docs/incoming/VM/PARALLEL-INPUT-FORWARDING.md` — the corrected design.
- `/home/user/Thurass/metaprogram/docs/incoming/VM/HANDOFF.md` — mission, settled facts, roadmap, pitfalls (§ refs below point here).
- Diagrams: `/home/user/Thurass/metaprogram/docs/incoming/VM/diagrams/architecture.svg`,
  `/home/user/Thurass/metaprogram/docs/incoming/VM/diagrams/mechanisms.svg`,
  `/home/user/Thurass/metaprogram/docs/incoming/VM/diagrams/reachability.svg`,
  `/home/user/Thurass/metaprogram/docs/incoming/VM/diagrams/loop.svg`.

> **Path convention.** Document/diagram references are full absolute paths under
> `/home/user/Thurass/metaprogram/docs/incoming/VM/`. Planned **implementation
> code** uses `<CODE_ROOT>/…` — a to-be-decided location (this docs folder is
> *not* the code root; pick `<CODE_ROOT>` in Phase 0, see §3).

---

## 1. Decision record (D1–D7)

Fill in **Choice** + **Rationale** + **Date** as each is made. Defaults/recommendations
are from `/home/user/Thurass/metaprogram/docs/incoming/VM/HANDOFF.md` §5–§6.

| # | Decision | Options | Recommended default | **Choice** | Rationale / date |
|---|---|---|---|---|---|
| D1 | Isolation boundary | VM · separate session (VD) | **VM** | _TBD_ | _____ |
| D2 | Hypervisor (if VM) | VirtualBox · Hyper-V · VMware | **VirtualBox** | _TBD_ | _____ |
| D3 | Mouse-look injection | in-guest `SendInput` · **guest virtual HID (relative)** · hypervisor rel-mouse | **guest virtual HID (relative)** | _TBD_ | _____ |
| D4 | Capture path | in-guest WGC stream · host-side WGC of VM window · GPU passthrough | **in-guest WGC stream** | _TBD_ | _____ |
| D5 | Transport / channel | vsock / Hyper-V sockets · VMCI · shared-mem · TCP (fallback) | **VM-native (vsock / Hyper-V sockets)** | _TBD_ | _____ |
| D6 | Policy | scripted (bring-up) → learned CNN → VLM | scripted → **CNN** | _TBD_ | _____ |
| D7 | Guest OS | Windows 11 (run Java Minecraft) | **Windows 11** | _TBD_ | _____ |

**Consequences to honor once chosen** (see `/home/user/Thurass/metaprogram/docs/incoming/VM/HANDOFF.md` §8):
- D3 = `SendInput` alone → Minecraft look-motion only works with the game's
  "Raw Input" option OFF; **virtual HID required** for the default (Raw Input ON).
- D1 = separate session → client single-console limit + disconnected-session
  lock/black-capture; needs `tscon` + virtual display + RDS GPU policy. Do **not**
  ship on RDPWrap/`termsrv.dll` patching.
- D2 = VirtualBox → mouse has **no** `VBoxManage` CLI; use the `IMouse` COM API.

---

## 2. Environment facts (record actuals)

| Item | Value |
|---|---|
| Host OS / build | _TBD_ |
| Hypervisor + version | _TBD_ |
| Guest OS / build | _TBD_ |
| Guest resolution (pinned) + DPI scaling | _TBD (pin it; disable scaling)_ |
| Channel endpoint (vsock port / pipe / TCP host:port) | _TBD_ |
| Minecraft edition + version + "Raw Input" setting | _TBD_ |
| Toolchain (host / guest compiler, SDK) | _TBD_ |

---

## 3. Planned repo layout (create in Phase 0)

> `<CODE_ROOT>` is the implementation-code root — **decide it in Phase 0** and
> record it here. It is **not** this docs folder
> (`/home/user/Thurass/metaprogram/docs/incoming/VM/`); e.g. `/home/user/Thurass/metaprogram/VM/`
> or a dedicated repo. **Chosen `<CODE_ROOT>`:** _TBD_

- `<CODE_ROOT>/host/` — process tracker (capture client), AI system, channel client.
- `<CODE_ROOT>/guest/` — process companion (injector), in-guest capturer, channel server.
- `<CODE_ROOT>/common/` — wire protocol, shared structs, action/event records.
- `<CODE_ROOT>/tools/input-probe/` — guest diagnostic that prints
  `WM_INPUT` + `GetAsyncKeyState` + message-queue events (ground truth for R2).

---

## 4. Phase 0 — Scaffolding

**Goal:** buildable skeleton both sides + a running VM.

- [ ] Record D1–D7 (§1 above) and environment facts (§2).
- [ ] Create the directory layout in §3.
- [ ] Provision the VM (D1/D2/D7); install the guest OS; install guest additions/tools.
- [ ] Pin guest resolution; disable DPI scaling (see `/home/user/Thurass/metaprogram/docs/incoming/VM/HANDOFF.md` §8).
- [ ] Host + guest build toolchains produce a hello-world each.
- [ ] Build `<CODE_ROOT>/tools/input-probe/` and run it in the guest.

**Acceptance:** VM boots; hello-world builds+runs on host and in guest; the
input-probe window shows live keyboard/mouse events when you type in the guest.

**Notes / result:** _____

---

## 5. Phase 1 — Input channel + keyboard proof-of-life

**Goal:** host tells the guest to press a key; the key genuinely registers.

- [ ] Implement transport (D5) in `<CODE_ROOT>/common/` — connect host↔guest.
- [ ] Define the wire protocol (key/mouse action records) in `<CODE_ROOT>/common/`.
- [ ] In-guest companion (`<CODE_ROOT>/guest/`) receives a "press A" action
      and injects via `SendInput` (keydown + keyup, correct scancode; use extended
      `e0` codes where needed — `/home/user/Thurass/metaprogram/docs/incoming/VM/HANDOFF.md` §8).
- [ ] Host client (`<CODE_ROOT>/host/`) sends the action over the channel.

**Acceptance (all three):**
1. The **input-probe** in the guest shows the keydown/keyup **and**
   `GetAsyncKeyState` reflects the key.
2. Notepad in the guest types "A".
3. Minecraft main-menu / chat receives the keystroke.

> If only (2) passes but not the `GetAsyncKeyState` leg of (1), the injection is
> message-only — fix before advancing (games poll async state).

**Notes / result:** _____

---

## 6. Later phases (detail in `/home/user/Thurass/metaprogram/docs/incoming/VM/HANDOFF.md` §7)

- **Phase 2 — Mouse-look:** guest virtual **relative** HID; accept = camera pans
  in Minecraft with **Raw Input ON** and the probe shows genuine `WM_INPUT`
  deltas (non-null `hDevice`).
- **Phase 3 — Observation:** in-guest WGC capture → host; measure capture→host latency.
- **Phase 4 — Close the loop (scripted):** scripted behavior runs in-game **while
  the user types normally on the host** (proves R1).
- **Phase 5 — Real policy:** learned policy + frame-stacking + latency-aware /
  action-repeat control (no in-band ACK; off-by-k).
- **Phase 6 — Robustness:** foreground watchdog, key-release fail-safe, frame
  de-dup + event-driven pacing, channel reconnect, clean teardown.

---

## 7. Running log

Newest first. One line per meaningful step (date · what · result).

- _(start here)_

## 8. Open questions / blockers

- _____
