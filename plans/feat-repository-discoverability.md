# Repository discoverability

## Acceptance criteria

The README identifies the board, links actual design, BOM, CubeMX and fabrication files, preserves the work-in-progress warning, and explains the missing external libraries and stackup discrepancy. GitHub has an accurate description and relevant topics. MIT applies to Michael Cutler's original work, with third-party exclusions. Hardware files and exports remain unchanged.

## Checklist

- [x] Inspect sources, history, README, libraries, and licence notices (completed: 2026-10-26).
- [x] Expand the README, scope MIT to original work, add licence text, and extend editor ignore rules (completed: 2026-10-26).
- [x] Set and verify GitHub description and topics (completed: 2026-10-26).
- [x] Check local Markdown links, ignore rules, whitespace, and the complete diff (completed: 2026-10-26; 16 local links resolve, design sources and exports unchanged).
- [x] Commit, push, and open [PR #1](https://github.com/makeristic/Feather_STM32WB55/pull/1) (completed: 2026-10-26).

## Findings and limits

No existing top-level licence was found. Vendor PDFs, library elements and third-party marks retain their existing terms. KiCad 5.1.7 is recorded in the PCB. The external STM32 symbol library and schematic cache are absent. The original notes specify 1mm thickness, while the PCB records 1.6mm. CubeMX input exists, but no application firmware or CircuitPython port is included. CAD and electrical validation are outside this documentation change.
