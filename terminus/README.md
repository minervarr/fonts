# Terminus

Economycs sets its entire interface in [Terminus](https://terminus-font.sourceforge.net/),
under the SIL Open Font License 1.1 (see `LICENSE`).

**No font file ships with this program.** Terminus is a *bitmap* font, so
`tools/bake_terminus.py` reads the installed strikes (`/usr/share/fonts/misc/ter-u*.otb`,
Arch package `terminus-font`) once and writes the glyphs into
`gui/font/terminus_font.hh` as one bit per pixel. That header is compiled in.

The consequences are the point:

- **No font library.** No FreeType, no msdfgen, no atlas generator, on desktop
  or on Android. `vk_canvas`'s MSDF engine is bypassed entirely — it needs Bézier
  outlines, and a bitmap font has none.
- **No asset file, no asset path, no loader.** 64 KB of `constexpr` arrays.
- **No antialiasing.** Not thresholded — *absent*. Terminus pixel values are
  strictly 0 or 255, verified when baking. This is what makes the two-colour
  rule exact rather than approximate.
- **Integer scaling only.** The strikes are 16 and 20 px; a phone draws them at
  2x or 3x with nearest sampling. A fractional scale would blur pixels into
  intermediate values and break the rule above, so it is never used.

Regenerate with `python3 tools/bake_terminus.py` (needs Pillow and the
`terminus-font` package). The output is checked in, so a clean clone builds
without either.
