# Repository discoverability

## Initial documentation acceptance criteria

The README identifies the board, links actual design, BOM, CubeMX and fabrication files, preserves the work-in-progress warning, and explains the missing external libraries and stackup discrepancy. GitHub has an accurate description and relevant topics. MIT applies to Michael Cutler's original work, with third-party exclusions. Hardware files and exports remain unchanged.

## Checklist

- [x] Inspect sources, history, README, libraries, and licence notices (completed: 2026-10-26).
- [x] Expand the README, scope MIT to original work, add licence text, and extend editor ignore rules (completed: 2026-10-26).
- [x] Set and verify GitHub description and topics (completed: 2026-10-26).
- [x] Check local Markdown links, ignore rules, whitespace, and the complete diff (completed: 2026-10-26; 16 local links resolve, design sources and exports unchanged).
- [x] Commit, push, and open [PR #1](https://github.com/makeristic/Feather_STM32WB55/pull/1) (completed: 2026-10-26).

## Initial documentation findings and limits

No existing top-level licence was found. Vendor PDFs, library elements and third-party marks retain their existing terms. KiCad 5.1.7 is recorded in the PCB. The external STM32 symbol library and schematic cache are absent. The original notes specify 1mm thickness, while the PCB records 1.6mm. CubeMX input exists, but no application firmware or CircuitPython port is included. The later source audit below adds static CAD checks and narrow source corrections; no bench validation is claimed.

## Follow-up source audit

The authorised follow-up extends this PR to source-level corrections supported by repository evidence and manufacturer documentation. Preserve historical formats and licensing, and do not claim board validation from static checks.

- [x] Compare schematic components, stored netlist, PCB references/pad nets, and fabrication provenance (completed: 2026-10-27).
- [x] Run KiCad nightly PCB DRC on temporary copies; distinguish historical/default-rule findings from proven defects (completed: 2026-10-27).
- [x] Verify relevant package/pin and power-interface assumptions against primary manufacturer sources (completed: 2026-10-27).
- [x] Apply and verify minimal supported corrections; record unresolved circuit and manufacturing work in `docs/code-audit-report.md` (completed: 2026-10-27).
- [x] Update README/PR scope, review the complete diff, commit, push, and return for root review before merge (completed: 2026-10-27; same PR #1, no merge performed by this agent).

## Independent validation follow-up

- [x] Reproduce globally registered legacy-library export omitting USB shield J5.S1 in nightly 10.99.0; confirm exact 213-pin graph equality with a new empty global configuration and the committed cache (completed: 2026-10-27).
- [x] Scope README, audit and PR validation claims to their actual library-resolution modes; preserve source geometry and document the apparent nightly inconsistency (completed: 2026-10-27).
