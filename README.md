# Kamen Rider Battride War Genesis (Sousei) - English patch (PS4)

Unofficial fan translation, Japanese to English, for the PS4 game `CUSA02716`, app v01.00.
This repository contains no game data, only binary patches against your own files. You need your own dump of the Japanese game.

> **PREVIEW v0.4.0. Not verified in game.**
> For this build the only test is an automated start to the title screen in shadPS4 0.21.0.
> Expect text that overflows its box, wrong line breaks and untested screens.

Download: the zip `battride-war-genesis-english-v0.4.0-preview.zip` on the Releases page of this repository.

## How this translation was made

Every English line was drafted by AI language models (Anthropic Claude) and then read again against the Japanese by a second AI edit pass. The tools, the glossary and the texture redraws were also made with AI agents, directed by the human maintainer. No human has proofread the whole text, and no human has played through it. Names follow the official English spelling where one exists; the rest is romanized. Mistakes in meaning, tone and names are therefore possible, and corrections are welcome (see "Report a problem").

## What's translated

- Menus and system messages
- Names and labels (riders, characters, forms, series, speakers)
- Story mode: mission info, mission briefings, in-mission dialogue and cutscene text
- Items, skills and the shop
- Figures and character info
- Battle voice lines (the shouts and quips during missions)
- 179 redrawn menu and HUD textures (labels baked into pictures)
- Credits and music lists, as a first draft only: some name readings are unsure

Not translated: the movies (their Japanese is part of the video), the trophies, and the text inside the game executable.

## Progress

| Version | What | State |
|---|---|---|
| v0.1 | Menus, system text, names and labels | Translated, edit-passed, in this release |
| v0.2 | Story mode (mission info, briefings, in-mission dialogue, cutscene text) | Translated, edit-passed, in this release |
| v0.3 | Items, skills, shop, figures, character info | Translated, edit-passed, in this release |
| v0.4 | Battle voice lines | Translated, edit-passed, in this release |
| v1.0 | Credits and music lists | First draft, edit pass not done (the draft is already in this release) |

"Edit-passed" means read by the second AI pass against the Japanese. It does not mean checked in game.

In numbers: 27,836 of 28,258 translated text cells (98.5%) have had the edit pass; the other 422 are the credits and music draft. 179 textures were redrawn in English. The glossary of fixed names and terms has 1,046 entries.

## What's next

1. Edit pass of the credits and music lists, then v1.0.
2. Checks in the running game that need players: text box sizes, the encrypted tables, whether battle voice lines are read from the character archives, and the redrawn textures (see "Known issues").
3. Not planned for now: the movies, the trophies, the text inside the executable.
4. A simpler way to apply the patch is being looked at.

## How to apply

What you need: your own dump of the game (PS4 `CUSA02716`, Japanese, app version 01.00, unmodified), already **extracted into a folder**. The folder must contain `nativeORBIS/` and `sce_sys/`. The patch does not extract the package for you. A game that is already patched, another version or a repacked dump is refused.

1. Unzip the download. It unpacks into one folder named `battride-war-genesis-english-v0.4.0-preview`. Open a terminal and `cd` into that folder; steps 3 and 4 are run from inside it. It holds `apply_kit.py`, the patch files and checksum lists.
2. Install xdelta3 and Python 3. On macOS: `brew install xdelta`. The script looks for `xdelta3` on your path and in the usual folders (`/opt/homebrew/bin`, `/usr/local/bin`, `/usr/bin`). If yours is elsewhere, add `--xdelta PATH` to the command in step 4.
3. Optional check that the download is intact, from inside that folder: `shasum -a 256 -c SHA256SUMS`. Every line should say `OK`.
4. Apply, still from inside that folder: `python3 apply_kit.py /path/to/CUSA02716`
   (`/path/to/CUSA02716` is the extracted game folder, not the folder you are in.)
   - The script first checks the SHA-256 of every original file. If one differs it writes **nothing** and names the file.
   - Otherwise it writes the patched files into a new folder next to the game folder, named like the game folder plus `-mods` (here `/path/to/CUSA02716-mods`), and checks each result. It never writes into the game folder. The optional `--out DIR` picks another output folder.
   - Exit code 0 means every file was patched and verified.
5. Start the game in shadPS4 from the game folder as usual, for example `./shadps4 -g /path/to/CUSA02716`. shadPS4 reads the `-mods` folder as an overlay, but only when its name is exactly the game folder name plus `-mods`. If the game still shows Japanese, check that name.
6. To undo the patch, delete the `-mods` folder. The game folder is not touched.

Back up your save data first. It is shared with the Japanese game.

shadPS4 notes:

- Tested only with shadPS4 0.21.0 on macOS (Apple M4). Other versions may read the overlay folder differently.
- The game needs the PS4 firmware modules in shadPS4's `user/sys_modules/` folder (26 modules). Without them the game crashed in our tests, with or without this patch. You must supply them; the patch does not contain them.
- The English uses the game's own font. It has no accented letters or long dashes, so the text avoids them. The patch does not change the font.

## Known issues

- Nothing has been checked in game as a whole. This build was only started automatically to the title screen. An early test build (2026-11-12, mostly texture redraws and one edited prompt, not this release) was looked at in game: the save-data prompt showed its English text (its button was still Japanese at that point, later replaced by a redrawn English one), and the redrawn mission HUD labels (`100 to defeat!`, `Now 0 Defeated!`, `COMBO`) showed in English. The mission dialogue box was still Japanese then. Nothing else was seen.
- Text box sizes were never measured. Long names and lines may run past the box, be cut off or overlap.
- Some text tables are encrypted in the game files. English that is longer than the Japanese has never been seen in game in those tables.
- Battle voice lines may still show Japanese if the game reads other copies of those lines stored in the character archives.
- Apart from the one button and the three HUD labels of that early test build, the 179 redrawn textures have never been seen in game. The vertical objective captions and the two Rider Road banner halves are the riskiest.
- Movies, trophies and executable text stay Japanese.
- Credits and music lists are a first draft. About 60 credit lines have unsure name readings.
- Some descriptions address the player as "you" and some do not; the style is not unified yet. A few descriptions lack the blank line between paragraphs.

## Report a problem

Open an issue in this repository. Please give:

- a screenshot,
- where in the game it is (which menu or mission),
- what the text should say,
- the version label: `v0.4.0-preview`.

Never attach game files.

## Licence and credits

- The `LICENSE` file (MIT) covers the apply script and this README.
- The translation text and the redrawn labels inside the patches are CC BY-NC-SA 4.0.
- The game, its names and its artwork belong to their owners. This project is not affiliated with them. The English labels in the redrawn textures are drawn with the Roboto font (SIL Open Font License 1.1, Copyright 2011 The Roboto Project Authors). The game's own font is not changed.
