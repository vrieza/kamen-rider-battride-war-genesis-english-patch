# Changelog

Each version's section is that release's notes. A section has a summary paragraph, `### Changes`, `### Tested` (what was run
before publishing) and `### Known issues` (only what is new or changed; the full list is in the [README](README.md#known-issues)).
Every build is a **preview** and is not verified in game. The version label is `vMAJOR.MINOR.PATCH-preview`: MINOR rises when a
domain of text is added, PATCH for fixes and for changes to the apply script.

## Planned

- **English patch for app v01.02**, the official update (cumulative, includes 01.01; adds three riders). It will be a delta next to the v01.00 patch; the v01.00 patch does not fit v01.02 and its apply script refuses that version. Planned, not started.

## 0.4.1

Same translation as 0.4.0, easier to apply: you no longer need xdelta3.

### Changes

- **The apply script decodes the patches itself.** `apply_kit.py` has a built-in VCDIFF decoder (Python standard library only), so
  Python 3.8 or newer is all you need. The `--xdelta` option is gone. The patches are still plain VCDIFF files, so a stock xdelta3 can decode
  them too.
- **README rewritten** with status, a table of what is translated, the shadPS4 settings we use and an optional 60 fps note.

### Tested

- The 15 patched files come out byte for byte identical to those of 0.4.0 (same original and patched SHA-256 in `manifest.csv`).
- Run with no xdelta3 on `PATH` and the system Python 3.9: 15 of 15 files in 0.5 s. A stock xdelta3 decodes the 15 patches to the same bytes.
- Not run: Python 3.8 (the stated minimum) and Windows.

### Known issues

- Unchanged from 0.4.0.

## 0.4.0

First public build. It carries the text of every domain from the internal milestones 0.1 to 0.4.

### Changes

- **Menus, system text, names and labels** (0.1): title and main menu, mode select, options, pause menu, save and install prompts, loading
  hints, tutorials; rider, character, enemy and form names, speakers, series names, Sound Gallery labels.
- **Story mode** (0.2): mission names and descriptions, briefings, in-mission cues and dialogue, cutscene text.
- **Items, skills, shop and figures** (0.3): skill and special-move names and effects, shop lines, figure entries, character info pages.
- **Battle voice lines** (0.4): the shouts and quips during missions (18,910 cells, the largest part).
- **179 redrawn textures** with English labels baked in (HUD, menus, result screens).
- **Credits and music lists** as a first draft (the edit pass is the plan for 1.0).

### Tested

- Every domain of 0.1 to 0.4 had a full AI edit pass against the Japanese, a lint run (0 errors) and a consistency check.
- A patched build starts to the title screen in shadPS4 0.21.0 (automated, no controller input).
- Nothing was played through.

### Known issues

- Text box sizes were never measured: long lines may overflow or be cut off.
- Battle voice lines may stay Japanese if the game reads the copies in the character archives.
- Movies, trophies and executable text are not translated.
