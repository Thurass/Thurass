# VM — Parallel Isolated Input Forwarding (design + handoff package)

Complete, self-contained package for the **bot-in-a-sandbox** project: an AI on
the host drives a game (e.g. Minecraft) in an isolated **VM/VD** through a
**parallel synthetic input channel** — no application APIs. **Design-only; no
implementation code yet.**

**Folder:** `C:\UserProgram\MetaProgram\docs\incoming\VM\` (repo-relative: `docs/incoming/VM/`)
**Branch:** `claude/virtual-desktop-input-forwarding-xmz6vf`

## Start here
1. `C:\UserProgram\MetaProgram\docs\incoming\VM\HANDOFF.md` — the full agent handoff (mission, settled facts, roadmap, pitfalls).
2. `C:\UserProgram\MetaProgram\docs\incoming\VM\PARALLEL-INPUT-FORWARDING.md` — the corrected design (source of truth).
3. `C:\UserProgram\MetaProgram\docs\incoming\VM\IMPLEMENTATION.md` — the live decision record + Phase 0/1 checklists to fill in.

## Contents

**Docs**
- `C:\UserProgram\MetaProgram\docs\incoming\VM\HANDOFF.md` — agent handoff (read first).
- `C:\UserProgram\MetaProgram\docs\incoming\VM\IMPLEMENTATION.md` — decision record + implementation log.
- `C:\UserProgram\MetaProgram\docs\incoming\VM\PARALLEL-INPUT-FORWARDING.md` — corrected design (VM/VD + virtual HID).
- `C:\UserProgram\MetaProgram\docs\incoming\VM\PARALLEL-INPUT-FORWARDING.html` — visual companion (self-contained; open in a browser).
- `C:\UserProgram\MetaProgram\docs\incoming\VM\VIRTUAL-DESKTOP-INPUT-FORWARDING.md` — HDESK "why-not" reference (superseded framing).
- `C:\UserProgram\MetaProgram\docs\incoming\VM\VIRTUAL-DESKTOP-INPUT-FORWARDING.html` — visual companion for the HDESK reference.

**Diagrams** (`C:\UserProgram\MetaProgram\docs\incoming\VM\diagrams\`)
- Corrected design: `architecture.svg`, `mechanisms.svg`, `reachability.svg`, `loop.svg`.
- HDESK reference: `taxonomy.svg`, `topology.svg`, `input-desktop.svg`, `injection-modes.svg`, `sequence.svg`, `lifecycle.svg`.

## Path conventions
- All references above are **full absolute paths** under this folder.
- The `.md`/`.html` files use **relative** `diagrams/…` links internally so they
  render on GitHub / in a browser — keep the `diagrams/` subfolder alongside them.
- Planned **implementation code** is referenced as `<CODE_ROOT>/…` (a to-be-decided
  location, **not** this docs folder — see `IMPLEMENTATION.md` §3).

## Not in this package
- `C:\UserProgram\MetaProgram\SCHEMATIC.md` — an **unrelated** iLOQ/TypeScript schematic;
  intentionally left at the repo root, not part of this VM package.
