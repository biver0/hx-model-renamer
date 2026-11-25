# HX Model Renamer

A one-page web app that renames the models on a Line 6 **HX Effects**, **HX Stomp** or **HX Stomp XL** (firmware 3.80.0), so the unit shows names like **Boss SD-1** instead of **Stupor OD**.

**Use it:** https://biver0.github.io/hx-model-renamer/

- Tick off the **Get ready** checklist (unit, HX Edit and Line 6 Updater, a backup, your setlist exported from HX Edit, the firmware file).
- Drop in your `.hxf` (stock 3.80.0, the [NAM A2 Lite](https://github.com/nocaseguy/hx-stomp-nam-lite) build, or a file you renamed here before).
- Edit names (16 characters max). Suggested names for effects follow the HX Effects manual's "Based On" list; amps, preamps and cabs follow helixhelp.com's model list. Line 6 Originals keep their names.
- Optionally add your exported setlist (`.hls`) or presets (`.hlx`), so their footswitch labels get the new names.
- Build: the page rewrites only model names, fixes every checksum, re-opens the result to check it, and gives you the new `.hxf` (plus your fixed presets).
- Install the firmware with Line 6 Updater, then import the fixed setlist (or presets) in HX Edit.

Everything runs in your browser. No firmware is uploaded, and none is included in this repo.

## Notes

- Unofficial and experimental. Not made or supported by Line 6. Install modified firmware at your own risk.
- Presets made before renaming keep Line 6's names on their footswitch labels (saved in the preset); new blocks get the new names. The page updates older presets' labels: export your setlist from HX Edit (`.hls`), add it in step 4, and import the fixed setlist in step 7. Single `.hlx` presets work too.
- HX Edit keeps showing Line 6's names (it has its own model list). Presets are unaffected: they store model IDs, not names.
- The NAM A2 Lite block's name is locked.
- Tested in software on all six files (stock and NAM A2 Lite for each unit): every checksum passes nocaseguy's verifier, only name bytes change, and setting the names back restores the original byte for byte. Installed on hardware so far: HX Effects (renamed firmware, plus a fixed setlist imported through HX Edit: unselected footswitches show the new names) and HX Stomp with NAM A2 Lite (renamed firmware, including amps, preamps and cabs). HX Stomp XL hasn't been tested on hardware yet.
- **Recovery:** start the unit in update mode and install that unit's stock 3.80.0 `.hxf` with Line 6 Updater. HX Effects: hold the right arrow (**>**) at power-on. HX Stomp / XL: hold **Page Right** at power-on (nocaseguy's README); Line 6's manual says footswitches 2 and 3.

Firmware layout details come from [nocaseguy/hx-stomp-nam-lite](https://github.com/nocaseguy/hx-stomp-nam-lite). Amp, preamp and cab "Based on" information comes from [helixhelp.com/models](https://helixhelp.com/models) by Jason Shimkoski. Product names are trademarks of their owners, used only to say what each model is based on.

## What changes

Each model has three names in the firmware, and the page sets all three:

1. its name in the model list,
2. its own name in the main application,
3. its **display name** in the model database.

New display names are added to the database's string table and each renamed model points to its new one. Nothing else in the database changes. Every checksum is recomputed: the application image CRC, the database string-table CRC, each archive entry's CRC32 and Fletcher sums, the payload MD5, and the size fields.

## Changelog

Versions follow major.minor.patch: a bug fix bumps the last number, a new feature the middle one. The page shows its version at the top, renamed files are named `…_Renamed_<version>.hxf`, and the page tells you which version renamed a file you drop in.

### 1.5.2 (2026-11-24)
- Works on HXtra builds (checked with HXtra 1.2.1 for the HX Stomp): the page opens them, renames them and every check passes, with NAM A2 Lite and HXtra's other changes untouched. HXtra's Real block names sets the list names but not the display names; building here sets those too.
- A file whose display names are still Line 6's is no longer described only as an old build of this page.
- The "not tested on this unit" note now shows only for the HX Stomp XL.

### 1.5.1 (2026-11-23)
- Fixed: if you had used the page before 1.5.0, the names it saved kept the amps, preamps and cabs at Line 6's names, so the new suggestions didn't show up and weren't built. The page now saves only the names you edit.

### 1.5.0 (2026-11-23)
- **Amps, preamps and cabs get suggested names** on the HX Stomp and XL (about 300 more), based on the "Based on" list at [helixhelp.com/models](https://helixhelp.com/models). Each one shows what it's based on in step 3. Line 6 Originals keep their names.
- Acoustic Sim gets a suggestion too (BOSS AC-2).
- Fixed: setting a model back to Line 6's name works when Line 6's display name is longer than 16 characters (Mandarin Bass 200).

### 1.4.0 (2026-11-23)
- **Setlists:** step 4 takes the setlist you export from HX Edit (`.hls`, every preset in slot order) and gives back a fixed setlist to import, so all your presets are updated in one go. Only footswitch labels change; every other byte of the presets stays as HX Edit wrote it, and the setlist's CRC32 and size are updated.
- Single presets (`.hlx`) are now edited the same way: only the label text changes.

### 1.3.0 (2026-11-22)
- The page now walks through everything in seven steps: **Get ready** (a checklist, after nocaseguy's setup page: unit, HX Edit and Line 6 Updater, backup, export your presets, firmware file), load firmware, name models, **add your presets**, build, install, **import your presets**.
- Presets are part of the build: add the `.hlx` files you exported, and step 5 gives you the renamed firmware and the fixed presets together, using the names you have at that moment.

### 1.2.0 (2026-11-22)
- **New: fix footswitch labels in older presets** (step 5). Export presets from HX Edit, drop the `.hlx` files on the page, and it changes every footswitch label that is still a stock Line 6 name to your new name. Labels you typed yourself, NAM A2 Lite and Line 6 Originals stay as they are. Import the fixed presets back onto their slots.

### 1.1.1 (2026-11-22)
- **Fixed:** each model's display name in the unit's model database is now renamed too (1.1.0 and earlier left it as Line 6's). If you built a file with 1.1.0 or earlier, rebuild it and reinstall; drop the old file on the page and it will tell you so.
- **Known limitation:** presets save each footswitch's label when its block is assigned, so presets made before renaming still show Line 6's names on the scribble strips of switches that aren't selected. Blocks you add from now on get the new names. Fixed for existing presets by 1.2.0's preset step.

### 1.1.0 (2026-11-22)
- Added HX Stomp and HX Stomp XL support (stock and NAM A2 Lite builds).

### 1.0.0 (2026-11-22)
- First release: HX Effects 3.80.0 (stock and NAM A2 Lite builds).
