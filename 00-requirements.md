# 00 — Requirements

Written before any schematic work. I have decided to note here every change, as well as noting the problems I'll encounter along the way.

**Revision:** A
**Date:** 12.08.2026

---

## 1. Purpose

A compact 12 V power distribution board for an FTC robot: one XT30 battery input
fanned out to three XT30 output branches. Functionally equivalent to the REV XT30
distribution block, but in a smaller footprint, targeted at our tight robot build
where the REV block occupies too much space.

## 2. System context (drives every current number below)

- Our robot runs from a single 12 V battery. The battery carries a **20 A in-line
  fuse that must be preserved** (FTC rule + gOBILDA Battery ships this way). This
  fuse is the absolute ceiling on total board input current and absolutley nothing downstream
  can exceed 20 A for more than the fuse's blow time.
- Our gOBILDA motors stall at ~10 A. 
- XT30 connectors are rated ~30 A continuous, so the connector is never the
  limiting factor; the PCB copper is.

## 3. Electrical requirements

| ID | Requirement | Value |
|---|---|---|
| ER-1 | Input connector | 1 × XT30 (board-mount), mates with battery XT30 |
| ER-2 | Input voltage | 12 V nominal (10–13 V operating range) |
| ER-3 | Input current ceiling | 20 A |
| ER-4 | Output connectors | 3 × XT30 (board-mount) |
| ER-5 | Per-branch rated current | **12.5 A continuous** |
| ER-6 | Copper temperature rise | ≤ 30 °C rise at rated current, worst-case branch |
| ER-7 | Voltage drop | ≤ 100 mV input-to-any-output at 12.5 A |
| ER-8 | Common ground | All V− pins commoned; all V+ pins commoned |

### Rationale for ER-5 (12.5 A per branch)

Sizing is done to worst-case, not typical, current as a trace sized for average
draw melts the one time a motor stalls. 12.5 A clears a stalled standard FTC
motor (~10 A) with margin. The three branches sum to 37.5 A theoretical, but the
20 A battery fuse (ER-3) means the board never actually carries that total as the
fuse blows first. So I had to design branches for 12.5 A each, input trunk designed
for 20 A.**

## 4. Mechanical requirements

| ID | Requirement | Value |
|---|---|---|
| 1 | Board footprint | Exactly half the area of one REV XT30 distribution block (27mm x 23.1mm x 11.7mm, 639.9mm^2) |
| 2 | Layer count | 2 |
| 3 | Copper weight | TBD — pending trace-width calculation (§ open questions). Likely 2 oz. |
| 4 | Connector orientation | All XT30 accessible without obstruction when board is mounted |

## 5. Success criteria

| ID | Criterion | Measurement method |
|---|---|---|
| SC-1 | Each branch carries 12.5 A continuously with ≤ 30 °C rise | Bench supply / electronic load, IR thermometer on the copper |
| SC-2 | Input-to-output drop ≤ 100 mV at 12.5 A | DMM across input and loaded output |
| SC-3 | All V+ outputs continuous with input; all V− commoned | DMM continuity |
| SC-4 | Board fits target footprint (½ REV block) | Physical measurement / caliper |
| SC-5 | No XT30 connector overheats at rated current | IR thermometer at connector solder joints |

## 6. Out of scope

- **Fusing per branch** — the battery's single 20 A fuse is the system protection;
  per-branch fusing is a possible Rev B feature, not Rev A.
- **Current/voltage sensing or telemetry** — this is a passive distribution board.
- **Switching / regulation** — pure passthrough, 12 V in = 12 V out.
