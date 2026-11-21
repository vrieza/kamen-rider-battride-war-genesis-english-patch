# Changelog

Each version's section is that release's notes. A section has a summary paragraph, `### Changes`, `### Tested` (what was run
before publishing) and `### Known issues` (only what is new or changed; the full list is in the [README](README.md#known-issues)).
Builds up to 0.4.2 were previews. From 1.0.0 the version label is `vMAJOR.MINOR.PATCH` (no `-preview`): MINOR rises when a
domain of text is added, PATCH for fixes and for changes to the apply script.

## 1.0.0 (2026-11-21)

First full release; the `-preview` label is dropped. Same translation as 0.4.2 for both app versions (v01.00 and v01.02), plus optional extras in both zips.

### Changes

- **`extras/dlc`**: static files that unlock all nine DLC add-ons on shadPS4 without a DLC dump (a `param.sfo` and an empty placeholder for each: Specter, Ghost Toucon Boost, Chaser, Hongo Shocker Combatman and five figure packs). Copy `extras/dlc/addcont` into the shadPS4 user folder.
- **`extras/60fps`**: a patch of `sysConf.boot` (frame cap 30.0 to 60.0), applied with `python3 apply_kit.py <game> --60fps`. Off by default.
- `install.md` explains both.

### Tested

- Unit tests pass; each zip unpacks, its `SHA256SUMS` match and `apply_kit.py` reproduces the built files on a clean dump; the v01.02 kit refuses a v01.00 dump.
- In game by the maintainer on shadPS4 0.21.0: the DLC unlock (all nine add-ons, the three DLC riders in missions) and 60 fps worked.

### Known issues

- Two figure-pack labels (`...02`, `...05`) use guessed ids.
- Everything else in the README's Known issues still applies (not every screen checked, credits draft, movies and trophies Japanese).

## 0.4.2

Executable text, and a second download for app v01.02.

### Changes

- **Text inside the game executable (`eboot.bin`).** Result screen, Rider Soul panel and popup, mission confirm dialog, HUD Shift Car and
  form names, pause Continue/Quit: 481 strings, written in place through the `-mods` overlay. The kit now also patches `eboot.bin`.
- **App v01.02 kit** (`v0.4.2-preview-v102`), a separate download for the official update (cumulative, includes 01.01). It carries the
  v01.00 translation (29,088 unchanged rows) plus about 700 new or changed lines for the three DLC riders (Chaser, Ghost Toucon Boost,
  Specter), 16 new glossary terms, two redrawn menu images, three new name plates, and the executable text moved onto the v01.02
  `eboot.bin` (plus one new string). Each kit refuses the other app version.

### Tested

- Unit tests pass; lint 0 errors; the executable rows check with 0 problems against each version's `eboot.bin`.
- App v01.00, in game on shadPS4 0.21.0 (run directly): Drive, Kuuga and Agito missions to the result screen, pause menu used, no crash;
  HUD names in English.
- App v01.02: automated start to the title screen only (app version 01.02, English title, patched `eboot.bin` loaded from `-mods`).
- Each zip was unpacked and applied to a clean dump; the result is byte for byte the tested build.

### Known issues

- **The v01.02 DLC riders were not tested.** The maintainer could not get a DLC dump to unlock them, so none of their text has been seen
  in game. Reports from DLC owners are welcome.
- Not every executable string has been seen on screen.
- Saves made on v01.02 may not load on v01.00 (the update's own note).

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
