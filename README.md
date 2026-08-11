# Board 02 — Compact XT30 Power Distribution Board

A 12 V power distribution board for an FTC robot: one XT30 battery input fanned
out to three XT30 branches, in half the footprint of the REV block it replaces.

| | |
|---|---|
| **Started** | 12/8/2026 |
| **Designer** | Vasii Vlad Andrei |
| **EDA tool** | KiCad 10 |
| **Layers** | 2 |
| **Per-branch rating** | 12.5 A continuous |
| **Input ceiling** | 20 A (battery fuse-limited) |
| **Fabricator** | TBD |

## Why this board exists

The REV XT30 distribution block works, but it's bigger than a good, tight robot build
can spare. This is a smaller replacement: same job, half the footprint.

The interesting part of this board isn't the circuit as it's a passive fan-out, there's
barely a "circuit" at all. It's the copper. At 12.5 A per branch and up to 20 A
on the input, ordinary signal traces would overheat and fail, and failing
on a robot mid-match is disastrous. So every power path on this board
is sized from an IPC-2221 calculation with a stated temperature-rise budget, and
that calculation is shown in the deisgn log.

## Result

<!-- Fill in after bring-up: photo, measured branch currents, measured temp rise,
     measured voltage drop. -->

_Not yet built._

## Key learnings

<!-- Fill in after the postmortem. Specific and technical. The trace-width
     decision, the copper-weight tradeoff, anything that surprised you at
     bring-up under load. -->

_Not yet built._

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
| `07-bringup/` | Power-on checklist and measured results |
| `08-test/` | Load-test plan and measurements vs. success criteria |
| `09-postmortem.md` | What failed, root causes, Rev B change list |

## License

Hardware: CERN-OHL-S-2.0. Documentation: CC-BY-4.0.
