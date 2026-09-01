

The REV XT30 distribution block works, but it's bigger than a good, tight robot build
can spare.

The interesting part of this board isn't the circuit as it's a passive fan-out, there's
barely a "circuit" at all. It's the copper. At 12.5 A per branch and up to 20 A
on the input, ordinary signal traces would overheat and fail, and failing
on a robot mid-match is disastrous. So every power path on this board
is sized from an IPC-2221 calculation with a stated temperature-rise budget, and
that calculation is shown in the deisgn log.


## Repository map

| Path | Contents |
|---|---|
| `00-requirements.md` | What the board must do, current ratings, and how success is measured |
| `01-design-log.md` | Dated log of every decision, calculation, and mistake |
| `02-component-selection/` | XT30 footprint choice, copper weight, datasheets |
| `03-schematic/` | KiCad project + schematic PDFs per revision |
| `04-layout/` | Stackup, trace-width calc results, DRC reports, 3D renders |
| `05-bom/` | Bill of materials |
| `06-assembly/` | Assembly photos and notes |
| `07-test/` | Load-test plan and measurements vs. success criteria |
| `08-postmortem.md` | What failed, root causes, Rev B change list |
