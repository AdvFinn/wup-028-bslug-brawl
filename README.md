# wup-028-bslug-brawl

**WUP-028 adapter BrainSlug module**
*by Alex "Chadderz" Chadwick*

This repository contains a BrainSlug module to allow support for the WUP-028 GCN
controller to USB adapter to arbitrary Wii games. At the time of writing I don't
quite recall what state it is in, other than that it basically works. To compile
you will first need to install BrainSlug (though not necessarily compile it).

---

## Brawl Support Extension
*by AdvFinn*

This fork adds GCN adapter support for Super Smash Bros. Brawl on vWii,
including a bypass for Brawl's disc integrity check (#001 error) that fires
when memory is patched at boot time.

### Changes from the original
- `my_start` now NOPs Brawl's #001 error call at `0x801d60a4` before patching
- Added `RSBE/pad.xml` with correct PADRead and PADInit patterns for Brawl
- PADRead pattern derived from Dolphin debugger analysis (entry at `0x80215fc4`)
- PADInit pattern confirmed via SI breakpoint analysis

### Known Limitations
- Rumble is non-functional; Brawl does not call `PADControlMotor` as a
  standalone function. The relevant addresses are documented in `RSBE/pad.xml`
  for future investigation.
  
### Compatibility
- **Project M** — untested. As a modified Brawl ISO it should use the same
  RSBE01 symbols, but this has not been verified. Contributions welcome.
- **[Project+](https://projectplusgame.com)** — requires using Project+'s own DOL as the alt DOL 
  from their launcher instead of brainslug's `boot.dol`. This has not been tested and may not be compatible
  since brainslug needs to be the entry point to apply patches before the game
  boots. Contributions and findings welcome.
- Brawl support has only been tested on NTSC-U (RSBE01). PAL (RSBP01) and
  NTSC-J (RSBJ01) have not been tested and may require different symbol addresses
  in their respective region folders. Contributions welcome.

---

## Credits
- [Alex "Chadderz" Chadwick](https://github.com/Chadderz121) — [brainslug-wii](https://github.com/Chadderz121/brainslug-wii) and [wup-028-bslug](https://github.com/Chadderz121/wup-028-bslug)
- [wilm0x42](https://github.com/wilm0x42) — [wii-gc-adapter-inject](https://github.com/wilm0x42/wii-gc-adapter-inject) GPF binary, used to identify the #001 bypass address and confirm PAD_Read entry point
- [riptl](https://github.com/riptl) — [wii-symbols](https://github.com/riptl/wii-symbols), provided the foundation for understanding brainslug's pattern-matching symbol format
