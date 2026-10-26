# Source and hardware audit

Reviewed 2026-10-26 with KiCad nightly 10.99.0. Scope: source/dependency recovery, schematic-to-PCB consistency, power/interface net inspection, physical-rule checks, and fabrication provenance. No electrical, RF, firmware, or manufacturing validation is claimed.

## Fixed: D10 shorted to ground

`Feather_STM32WB55.kicad_pcb:3282` placed a 0.45 mm GND via at `(164.45,88.65)`, overlapping the 0.2 mm D10 track at `y=88.9` on B.Cu. Their centre-to-centre distance was 0.25 mm, less than the 0.325 mm sum of copper radii. KiCad DRC reproduced the GND/D10 short.

Moved that via to `(164.45,88.4)` and centred its front-layer GND segment endpoint on the new location. An otherwise identical before/after DRC with zone refill removed **only that short**, introduced **no new findings**, and retained **0 unconnected items**. The comparison used the same temporary legacy project context and no configured global footprint tables: 283 findings before, 282 after. This demonstrates the local correction; it does not make the entire board manufacturing-ready.

## Other corrections made

- Restored missing STM32 and OPL switch symbols from the project's original `e27ee62` schematic cache, removed in `e6276cd`. Recovered their footprints from the placed PCB modules, stripping instance/net data and normalising placement rotation while retaining geometry and pad numbering. See [library provenance](../libraries/README.md).
- Added project library tables and a versioned complete legacy symbol cache. Standard symbols use [KiCad tag 5.1.7](https://github.com/KiCad/kicad-symbols/tree/5.1.7), commit `bf475af94877e8fd9cf80e667578ff61835e02bb`. The KiCad community's [licence and exception](../LICENSES/KiCad-Libraries.md) are preserved, and recovered mixed-source libraries are excluded from the original-work MIT grant.
- Qualified ANT1/FL1 footprint identifiers consistently in the schematic, netlist, BOM, and PCB. Fixed three project-specific 3D-model paths to the sibling Makeristic library checkout.
- Restored PCB references `J3` and `U5`, previously changed to `SWD` and `FLASH`, to match the schematic/BOM without moving pads or changing their nets.
- Removed two unattached no-connect flags and one floating GND annotation. Fresh netlist comparison confirms these orphan annotations did not carry circuit connectivity.

## Remaining engineering concerns

**PCB clearance and footprint review remains necessary.** The recovered U3 footprint has a 5.7 × 5.7 mm exposed pad, and modern DRC reports about 0.0964 mm to several signal pads, below the board's 0.127 mm netclass clearance. Confirm the complete land pattern, paste strategy, and solder-mask process against the [STM32WB55CG datasheet](https://www.st.com/resource/en/datasheet/stm32wb55cg.pdf), rather than replacing the footprint or changing clearances blindly. Other track/connector-hole, courtyard, mask-bridge, and edge findings remain.

**The original symbol is electrically weak for ERC.** Its STM32 pin types are `Unspecified`; restoring the original data does not supply verified pin types. Validate any future electrical-type changes against ST's pin definitions before using ERC as an electrical sign-off.

**Stackup intent is unresolved.** The `.pro` file (`BoardThickness=1.6`) and PCB (`thickness 1.6`) agree, including the earliest PCB commit inspected; the later README says 1 mm. Both source files remain 1.6 mm. Confirm the actual manufactured/intended four-layer stackup and RF impedance calculation before changing thickness or ordering.

The QSPI flash circuit connects only IO0/IO1 and straps WP/HOLD high, consistent with the original dual-I/O description rather than a completed four-data-line firmware implementation. USB D+/D−, SWD and power nets were traced through the stored netlist and compared with PCB pads, but timing, supply transients, battery charging, RF matching, and antenna performance require engineering review and bench measurements.

## Verification

Fresh schematic export succeeds with the restored cache. Its complete pin-connectivity graph matches the stored netlist across **213 pins** after ignoring generated net-name spelling changes. All 45 schematic components have matching PCB references, values, footprints, and pad-net assignments; board-only mounting holes and graphics are excluded from that component comparison. Both recovered symbol libraries load through the CLI, and both recovered footprint libraries successfully export to SVG.

With isolated tables for historical symbols, installed modern footprints and project libraries, ERC reports **58 findings**: 48 unspecified-pin pairings, 3 undriven input expectations, 4 supply-drive declarations, and 3 multiple-net-name warnings. The orphan label/no-connect findings are gone.

Final refilled DRC in that configured environment reports **280 findings**, **0 shorts**, and **0 unconnected items**: 48 clearance, 32 copper/edge, 9 hole-clearance, 46 modern-library footprint differences, 116 solder-mask bridges, 8 courtyard overlaps, 4 incomplete thermal connections, and 17 other courtyard/text/silkscreen findings. The counts differ from the controlled short-fix comparison because library configuration and historical project-context loading affect the rule report. Legacy zone conversion is explicitly warned by nightly KiCad; no errors or exclusions were suppressed.

Representative commands, run on temporary copies:

```sh
kicad-cli-nightly sch export netlist --output /tmp/feather.net Feather_STM32WB55.sch
kicad-cli-nightly sch erc --format json --severity-all --exit-code-violations --output /tmp/feather-erc.json Feather_STM32WB55.sch
kicad-cli-nightly pcb drc --format json --severity-all --refill-zones --exit-code-violations --output /tmp/feather-drc.json Feather_STM32WB55.kicad_pcb
```

ERC/DRC return exit 5 because findings remain. Audit-only library tables used temporary `XDG_CONFIG_HOME`; no shared configuration changed. Local Markdown links and project-library targets were checked, and whitespace checks pass.

## Fabrication status

The source fix is **not present in the existing Gerbers or drill files**. Those exports, the PDF, and renders remain historical snapshots and must not be used as a validated manufacturing release. Refill zones in the chosen supported KiCad version, resolve outstanding engineering work, and regenerate/review the whole fabrication set together. No application firmware, CircuitPython port, flashing procedure, or electrical/RF test report is included.
