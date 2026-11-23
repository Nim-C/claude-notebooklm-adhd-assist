# claude-notebooklm-adhd-assist

Study tools for **NotebookLM + Claude**, shaped for an ADHD brain. Upload one file to Claude and you get three skills:

| Skill | What it does | When it runs |
| --- | --- | --- |
| `notebooklm-adhd-notebook` | Opens NotebookLM in Chrome, creates a new notebook and sets its chat to ADHD-style answers (answer first, short numbered steps, nothing important cut). | When you ask Claude to create a NotebookLM notebook with ADHD rules. Needs the Claude in Chrome extension and a Google sign-in. |
| `summary-adaptation` | Turns a NotebookLM summary (or any study material) into a Hebrew study page: bottom line first, numbered steps, reading time per part, nothing skipped. | When you ask for a summary or to adapt study material, or type `/summary-adaptation`. |
| `notebooklm-adhd-settings` | Shows and changes one choice: should ADHD mode turn on automatically when you use the NotebookLM tools? Always / only apply the rules to the page / ask each time. | Type `/notebooklm-adhd-settings`. The first time you use a NotebookLM tool, you are asked this automatically. |

## Requirement: the ADHD plugin

This plugin needs the **adhd-mode** plugin. Install it first:

- Claude chat: **[claude-chat-adhd-assist](https://github.com/Nim-C/claude-chat-adhd-assist)**
- Claude Code: **[claude-code-adhd-assist](https://github.com/Nim-C/claude-code-adhd-assist)**

`summary-adaptation` loads the ADHD rules from `adhd-mode:adhd-on` each time it runs, so when you update the ADHD plugin, summaries follow the new rules with no change here. Without the ADHD plugin it stops and tells you to install it. `plugin.json` declares this as a dependency (`adhd-mode@claude-code-adhd-assist`).

## Install (one file)

1. Install the ADHD plugin (see above).
2. Download **[notebooklm-adhd-notebook.zip](notebooklm-adhd-notebook.zip)** (open it, then click the download button).
3. In Claude, open **Settings** → **Capabilities** → **Skills**.
4. Click **Upload skill** and choose `notebooklm-adhd-notebook.zip`.

If you do not see Upload skill, turn on **Code execution** on the same screen first.

## Notes

- `summary-adaptation` always applies the ADHD rules to the summary page. Whether ADHD mode also turns on in the chat is your choice (see `/notebooklm-adhd-settings`).
- Where the choice is kept: in Claude Code, in `~/.claude/notebooklm-adhd-settings.json`. In the Claude chat, in Claude's memory when memory is on; otherwise you are asked again in each new chat.
- The zip holds the same files you see in this repository.

## Credits

The ADHD rules are adapted from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) (MIT License, see `LICENSE.txt`). Not made by Anthropic or Google. It changes how answers are formatted; it does not diagnose or treat anything.
