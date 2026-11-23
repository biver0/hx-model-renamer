# HX Model Renamer

A one-page web app that renames the effect models on a Line 6 **HX Effects** (firmware 3.80.0), so the unit shows names like **Boss SD-1** instead of **Stupor OD**.

**Use it:** https://biver0.github.io/hx-model-renamer/

- Drop in your `.hxf` (stock 3.80.0, the [NAM A2 Lite](https://github.com/nocaseguy/hx-stomp-nam-lite) build, or a file you renamed here before).
- Edit names (16 characters max). Suggested names follow the HX Effects manual's "Based On" list.
- Build: the page rewrites only the name fields, fixes every checksum (image CRC, archive CRC32 and Fletcher sums, payload MD5), re-opens the result to check it, and gives you the new `.hxf`.

Everything runs in your browser. No firmware is uploaded, and none is included in this repo.

## Notes

- Unofficial and experimental. Not made or supported by Line 6. Install modified firmware at your own risk.
- HX Edit keeps showing Line 6's names (it has its own model list). Presets are unaffected: they store model IDs, not names.
- The NAM A2 Lite slot (Xenomorph Fuzz Mono) is locked.
- HX Stomp isn't supported yet.
- **Recovery:** hold the right arrow (**>**) while powering on the HX Effects, then install the stock `HX_Effects_v3.80.0_0xd97239907.hxf` with Line 6 Updater.

Firmware layout details come from [nocaseguy/hx-stomp-nam-lite](https://github.com/nocaseguy/hx-stomp-nam-lite). Product names are trademarks of their owners, used only to say what each model is based on.
