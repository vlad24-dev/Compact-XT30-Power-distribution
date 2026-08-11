# 00 — Requirements

Written before any schematic work. Every later decision must trace back to a line
in this document, or it is arbitrary.

**Revision:** A
**Date:** FILL IN

---

## 1. Purpose

A compact 12 V power distribution board for an FTC robot: one XT30 battery input
fanned out to three XT30 output branches. Functionally equivalent to the REV XT30
distribution block, but in a smaller footprint — targeted at tighter robot builds
where the REV block does not fit.

## 2. System context (drives every current number below)

- FTC robots run from a single 12 V battery. The battery carries a **20 A in-line
  fuse that must be preserved** (FTC rule + REV Slim Battery ships this way). This
  fuse is the absolute ceiling on total board input current — nothing downstream
  can exceed 20 A for more than the fuse's blow time.
- Common FTC motors (REV HD Hex / NeveRest / goBILDA, RS-555 type) stall at
  ~10 A. Heavier gearmotors can reach ~19 A stall.
- XT30 connectors are rated ~30 A continuous — so the connector is never the
  limiting factor; the PCB copper is.

## 3. Electrical requirements

| ID | Requirement | Value |
|---|---|---|
| ER-1 | Input connector | 1 × XT30 (board-mount), mates with battery XT30 |
| ER-2 | Input voltage | 12 V nominal (10–13 V operating range) |
| ER-3 | Input current ceiling | 20 A (fuse-limited at the battery) |
| ER-4 | Output connectors | 3 × XT30 (board-mount) |
| ER-5 | Per-branch rated current | **12.5 A continuous** |
| ER-6 | Copper temperature rise | ≤ 30 °C rise at rated current, worst-case branch |
| ER-7 | Voltage drop | ≤ 100 mV input-to-any-output at 12.5 A |
| ER-8 | Common ground | All V− pins commoned; all V+ pins commoned |

### Rationale for ER-5 (12.5 A per branch)

Sizing is done to worst-case, not typical, current — a trace sized for average
draw melts the one time a motor stalls. 12.5 A clears a stalled standard FTC
motor (~10 A) with margin. The three branches sum to 37.5 A theoretical, but the
20 A battery fuse (ER-3) means the board never actually carries that total — the
fuse blows first. So: **branches designed for 12.5 A each, input trunk designed
for 20 A.**

## 4. Mechanical requirements

| ID | Requirement | Value |
|---|---|---|
| MR-1 | Board footprint | Exactly half the area of one REV XT30 distribution block (MEASURE the REV block and record its dimensions here before designing) |
| MR-2 | Layer count | 2 |
| MR-3 | Copper weight | TBD — pending trace-width calculation (§ open questions). Likely 2 oz. |
| MR-4 | Thickness | 1.6 mm |
| MR-5 | Mounting | TBD — match robot mounting pattern; record hole spec here |
| MR-6 | Connector orientation | All XT30 accessible without obstruction when board is mounted |

## 5. Success criteria — how "it works" is measured

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

## 7. Open questions — resolve before layout

- [ ] MR-1: measure the REV block, compute the ½-area target, record it here.
- [ ] MR-3: run the IPC-2221 trace-width calculation for 12.5 A (branch) and 20 A
      (input) at 10 °C and 30 °C rise, for both 1 oz and 2 oz copper. Decide copper
      weight and whether power paths are traces, pours, both-layers-stitched, or
      exposed-copper. **This is the core engineering decision of the board.**
- [ ] MR-5: confirm robot mounting hole pattern.
- [ ] ER-1/ER-4: choose the specific board-mount XT30 footprint and verify against
      the real connector's datasheet before locking it in.
