# HX Model Renamer

A one-page web app that renames the models on a Line 6 **HX Effects**, **HX Stomp** or **HX Stomp XL** (firmware 3.80.0), so the unit shows names like **Boss SD-1** instead of **Stupor OD**.

**Use it:** https://biver0.github.io/hx-model-renamer/

- Drop in your `.hxf` (stock 3.80.0, the [NAM A2 Lite](https://github.com/nocaseguy/hx-stomp-nam-lite) build, or a file you renamed here before).
- Edit names (16 characters max). Suggested names for effects follow the HX Effects manual's "Based On" list; amps, preamps and cabs keep Line 6's names unless you change them.
- Build: the page rewrites only the name fields, fixes every checksum (image CRC, archive CRC32 and Fletcher sums, payload MD5), re-opens the result to check it, and gives you the new `.hxf`.

Everything runs in your browser. No firmware is uploaded, and none is included in this repo.

## Notes

- Unofficial and experimental. Not made or supported by Line 6. Install modified firmware at your own risk.
- HX Edit keeps showing Line 6's names (it has its own model list). Presets are unaffected: they store model IDs, not names.
- The NAM A2 Lite block's name is locked.
- Tested in software on all six files (stock and NAM A2 Lite for each unit): every checksum passes nocaseguy's verifier, only name bytes change, and setting the names back restores the original byte for byte. Installed on hardware so far: HX Effects.
- **Recovery:** start the unit in update mode and install that unit's stock 3.80.0 `.hxf` with Line 6 Updater. HX Effects: hold the right arrow (**>**) at power-on. HX Stomp / XL: hold **Page Right** at power-on (nocaseguy's README); Line 6's manual says footswitches 2 and 3.

Firmware layout details come from [nocaseguy/hx-stomp-nam-lite](https://github.com/nocaseguy/hx-stomp-nam-lite). Product names are trademarks of their owners, used only to say what each model is based on.
