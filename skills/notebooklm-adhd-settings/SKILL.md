---
name: notebooklm-adhd-settings
description: "Shows and changes whether ADHD mode turns on automatically when the NotebookLM tools are used. Use when the user types /notebooklm-adhd-settings, or when another skill of this plugin sends you here for the choice check."
---

# NotebookLM + ADHD settings

One setting: what happens to ADHD mode (the `adhd-mode` plugin) when the user uses `notebooklm-summary-adaptation`.

| Value | Meaning |
| --- | --- |
| `always` | Turn ADHD mode on, exactly as `/adhd-on` does, then continue. |
| `rules-only` | Do not turn ADHD mode on. Apply the ADHD rules to the summary page only. |
| `ask` | Ask "Turn ADHD mode on now? (yes / no)" each time, and follow the answer for this time only. |

Write everything to the user in the language they write in.

## Where the choice is kept

Read it in this order; the first one found wins:
1. Claude Code (you can read files): `~/.claude/notebooklm-adhd-settings.json`, shaped `{ "adhd": "always" | "rules-only" | "ask" }`.
2. Claude's memory, or earlier in this chat: a line "NotebookLM + ADHD choice: <value>".
3. Nothing found: the choice is "not chosen yet".

Saving a new choice:
- Claude Code: write the file above.
- Claude chat: save "NotebookLM + ADHD choice: <value>" to memory if a memory tool is available. If not, it holds for this chat only; say so in one line, and suggest the user tell Claude "remember: NotebookLM + ADHD choice: <value>".

## /notebooklm-adhd-settings

Show the current value and the options, exactly in this shape, nothing else:

```
NotebookLM + ADHD: <🔵 always on | ⚪ rules on the page only | ❔ ask each time | not chosen yet>

Options:
  1. Always turn ADHD mode on
  2. Don't turn it on, only apply the rules to the page
  3. Ask me each time
```

When the user answers 1, 2 or 3: save `always`, `rules-only` or `ask`, then confirm in one line, for example `NotebookLM + ADHD: ⚪ rules on the page only`.

## Choice check (used by the other skills of this plugin)

1. Read the choice as above.
2. Not chosen yet: show the `/notebooklm-adhd-settings` screen above, with this first line instead: "First time using the NotebookLM tools. Turn ADHD mode on automatically?" Wait for 1, 2 or 3, save it, then go on.
3. `always`: load `adhd-mode:adhd-on` and do what it says (one line "🔵 ADHD: ON", then ADHD mode stays on in this chat). If ADHD mode is already on in this chat, do nothing.
4. `rules-only`: change nothing in the chat.
5. `ask`: ask "Turn ADHD mode on now? (yes / no)". Yes: as in 3. No: as in 4.
6. Then return to the skill that sent you here and continue it.

Never change the choice unless the user picks a new one. `/adhd-off` still turns ADHD mode off at any time.
