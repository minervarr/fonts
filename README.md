# fonts

The shared typeface set for the `~/Files/code/active` workspace. Every GUI app
mounts this repo as a submodule at `assets/fonts`, so a font path is the same
string in every project and the 127 MB is stored once instead of once per repo.

## Families

| Directory | Covers | Format | Upstream licence |
|---|---|---|---|
| `fandol/` | Chinese (Simplified) | OTF | GPL-2.0 with font exception |
| `haranoaji/` | Japanese | OTF | OFL-1.1 |
| `unfonts-core/` | Korean | TTF | Un-fonts licence (BSD-like) |
| `newcomputermodern/` | Latin, Greek, Cyrillic, Devanagari, math | OTF | OFL-1.1 / GPL-3.0 |
| `terminus/` | bitmap terminal faces, 12–32 px | OTB | OFL-1.1 (see `terminus/LICENSE`) |
| `ui/` | the single-file UI face used by AOAS and navaLauncher | OTF | see upstream |

`terminus/` ships the bitmap `.otb` strikes. Economycs additionally embeds
Terminus directly in source (`gui/font/terminus_font.hh`); the licence here
covers both uses.

## Using it

    git submodule add https://github.com/minervarr/fonts assets/fonts
    git submodule update --init --recursive

Paths are then stable across the workspace:

    assets/fonts/newcomputermodern/NewCM10-Regular.otf
    assets/fonts/fandol/FandolSong-Regular.otf
    assets/fonts/haranoaji/HaranoAjiMincho-Regular.otf
    assets/fonts/unfonts-core/UnBatang.ttf
    assets/fonts/terminus/ter-u16n.otb
    assets/fonts/ui/ui.otf

## What is deliberately not here

App icon fonts. They look like a typeface but they are artwork: the glyphs are
per-application drawings in the Private Use Area, and the repos do not agree on
them — streamer's `matrix-icons.otf` is a different file from the one Matrix
Player, ViewMage and ImagesLogosCreator share, under the same name. Sharing
them would silently swap one app's icons for another's. Each repo keeps its own
at `assets/icons/`.

## Do not

Do not copy families out of here into a consumer's own tree — that is the
duplication this repo exists to remove. Consumers select the handful of faces
they actually ship at build time and copy *those* into their runtime assets
directory; they do not vendor the whole set into an APK.
