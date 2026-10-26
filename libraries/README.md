# Recovered project libraries

These two symbols were recovered from `Feather_STM32WB55-cache.lib` in commit `e27ee62` (before its removal by `e6276cd`). The STM32WB55 and OPL switch footprints were recovered from the corresponding placed modules in the committed PCB.

The library nicknames match the original schematic. Cached symbol identifiers have been restored to their original library names; symbol geometry, pin numbers, pin names, and electrical types are unchanged. Footprints retain the original local geometry and pad numbering, with board position, net assignments, and instance references removed and instance rotation normalised. The STM32 3D-model path now points to the sibling Makeristic library checkout.

These assets are recovered historical dependencies, not newly designed or verified replacements. The original cached STM32 symbol marks its pins unspecified, and the footprint still requires land-pattern/clearance review described in the [audit](../docs/code-audit-report.md). Recovered third-party library material is excluded from Michael's MIT grant; its original owners' terms apply, and no additional licence is asserted here.
