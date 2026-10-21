---
name: shoty
description: Drive Shoty, the desktop video editor, from the shell with the `shoty` command — open or create projects, import media, cut the timeline, add captions and color, look at frames, and export finished videos. Use whenever the user mentions Shoty (쇼티) or asks to make, edit, or export a video with Shoty on this computer, e.g. "shoty 써서 영상 뽑아봐".
---

# Shoty

Shoty is a video editor installed on this computer. The `shoty` command drives
it: every editing ability Shoty's own agent has is a `shoty` subcommand, and
every subcommand prints one JSON object. Work through `shoty`. Do not search for
Shoty's source code, edit project files by hand, or build the video with ffmpeg
instead.

## Start

1. Run `shoty --help` once. It prints the command guide as plain text.
2. If `shoty` is not found, or a command exits 3 saying Shoty is not accepting
   command-line control, ask the user to open Shoty → Preferences → Advanced
   and turn on "Allow command-line control" (환경 설정 → 고급 → 명령줄 제어
   허용), then try again. Do not look for another way in.
3. Pick the project:
   - `shoty projects` lists the projects on this computer;
     `shoty open <project-id|folder>` starts a session in one.
   - `shoty new "<name>" [--size 1920x1080] [--fps 30]` starts a session in a
     new project.
4. Read the briefing file that `open` or `new` prints before anything else. It
   is the manual Shoty gives its own agent, and the project as it is now: ids,
   tracks, and media.

## Work

- `shoty tools [word]` finds tools, for example `shoty tools import`,
  `shoty tools caption`, `shoty tools export`. `shoty help <tool>` shows a
  tool's flags, types, and an example.
- `shoty <tool> --flag value ...` runs a tool.
  `shoty call <tool> '<json>'` runs it with raw JSON arguments.
- Video times are timecodes `HH:MM:SS:FF` on the sequence's own frames.
- Look before you say a shot is right. Tools that show frames save the pictures
  as files and list their paths under `images`; open those files and check them.
- Exit codes: `0` done · `1` the tool refused or failed — read `error` and
  `hint`, fix the call, retry · `2` usage · `3` Shoty unreachable · `4` waiting
  for approval.
- Exit `4` means a card waits for the user: a paid generation or a staged edit.
  Tell the user what is waiting and where. Run `shoty approve <card>` only when
  the user has told you to go ahead; `shoty reject <card>` declines. Never
  approve a card just to get unstuck.

## Finish

`shoty close --summary "<what you did>"` saves the project and ends the
session; the summary stays in the project's chat in Shoty. Tell the user where
the exported file is.
