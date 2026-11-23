# HX Model Renamer

A one-page web app that renames the models on a Line 6 **HX Effects**, **HX Stomp** or **HX Stomp XL** (firmware 3.80.0), so the unit shows names like **Boss SD-1** instead of **Stupor OD**.

**Use it:** https://biver0.github.io/hx-model-renamer/

- Drop in your `.hxf` (stock 3.80.0, the [NAM A2 Lite](https://github.com/nocaseguy/hx-stomp-nam-lite) build, or a file you renamed here before).
- Edit names (16 characters max). Suggested names for effects follow the HX Effects manual's "Based On" list; amps, preamps and cabs keep Line 6's names unless you change them.
- Build: the page rewrites only model names, fixes every checksum, re-opens the result to check it, and gives you the new `.hxf`.

Everything runs in your browser. No firmware is uploaded, and none is included in this repo.

## Notes

- Unofficial and experimental. Not made or supported by Line 6. Install modified firmware at your own risk.
- HX Edit keeps showing Line 6's names (it has its own model list). Presets are unaffected: they store model IDs, not names.
- The NAM A2 Lite block's name is locked.
- Tested in software on all six files (stock and NAM A2 Lite for each unit): every checksum passes nocaseguy's verifier, only name bytes change, and setting the names back restores the original byte for byte. Installed on hardware so far: HX Effects.
- **Recovery:** start the unit in update mode and install that unit's stock 3.80.0 `.hxf` with Line 6 Updater. HX Effects: hold the right arrow (**>**) at power-on. HX Stomp / XL: hold **Page Right** at power-on (nocaseguy's README); Line 6's manual says footswitches 2 and 3.

Firmware layout details come from [nocaseguy/hx-stomp-nam-lite](https://github.com/nocaseguy/hx-stomp-nam-lite). Product names are trademarks of their owners, used only to say what each model is based on.

## What changes

Each model has three names in the firmware, and the page sets all three:

1. its name in the model list,
2. its own name in the main application,
3. its **display name** in the model database, which the footswitch scribble strips show.

New display names are added to the database's string table and each renamed model points to its new one. Nothing else in the database changes. Every checksum is recomputed: the application image CRC, the database string-table CRC, each archive entry's CRC32 and Fletcher sums, the payload MD5, and the size fields.

## Changelog

Versions follow major.minor.patch: a bug fix bumps the last number, a new feature the middle one. The page shows its version at the top, renamed files are named `…_Renamed_<version>.hxf`, and the page tells you which version renamed a file you drop in.

### 1.1.1 (2026-11-22)
- **Fixed:** on the unit, footswitches that weren't selected still showed Line 6's names on their scribble strips (only the selected block showed the new name). The firmware keeps a third copy of each name, the display name in its model database, and the page now renames that too.
- **If you built a file with 1.1.0 or earlier, rebuild it and reinstall.** Drop the old file on the page and it will tell you so; your names load as they were.

### 1.1.0 (2026-11-22)
- Added HX Stomp and HX Stomp XL support (stock and NAM A2 Lite builds).

### 1.0.0 (2026-11-22)
- First release: HX Effects 3.80.0 (stock and NAM A2 Lite builds).
