# claude-notebooklm-adhd-assist

Study tools for **NotebookLM + Claude**, shaped for an ADHD brain. NotebookLM stays as it is; the ADHD adaptation happens in Claude, when it reads the summary from your notebook. You get two skills:

| Skill | What it does | When it runs |
| --- | --- | --- |
| `notebooklm-summary-adaptation` | Takes the summary NotebookLM gave you in your notebook and turns it into a study page in the language you want (by default, the language you write in): bottom line first, numbered steps, reading time per part, nothing skipped. It asks for your notebook link and reads the summary from it in Chrome. | Type `/notebooklm-summary-adaptation` in a new chat, or ask to adapt a NotebookLM summary. Needs the Claude in Chrome extension and a Google sign-in. |
| `notebooklm-adhd-settings` | Shows and changes one choice: should ADHD mode turn on automatically when you adapt a NotebookLM summary? Always / only apply the rules to the page / ask each time. | Type `/notebooklm-adhd-settings`. The first time you adapt a summary, you are asked this automatically. |

## Install in Claude Code: just ask Claude

Tell Claude Code:

> Install the plugin from https://github.com/Nim-C/claude-notebooklm-adhd-assist

That is all. The ADHD plugin it needs is installed with it.

**For Claude (do this when asked to install from this repository):** run these two commands yourself, in this order. Do not ask the user to run them.

```
claude plugin marketplace add Nim-C/claude-code-adhd-assist
claude plugin install notebooklm-adhd-notebook@claude-code-adhd-assist
```

The second command also installs the dependency `adhd-mode@claude-code-adhd-assist`. If it is already installed, it is reused, not installed twice. Then tell the user in one line that the plugins are installed and take effect in a new session (or after `/reload-plugins`).

By hand, the same thing from a shell: `claude plugin install notebooklm-adhd-notebook --marketplace Nim-C/claude-code-adhd-assist`.

## Install in the Claude chat (two uploads)

The Claude chat cannot install plugins by itself, so here you upload two separate files, the ADHD plugin first:

1. From **[claude-chat-adhd-assist](https://github.com/Nim-C/claude-chat-adhd-assist)**, download `adhd-mode-plugin.zip`. Skip this if you already have it.
2. From this repository, download **[notebooklm-adhd-notebook.zip](notebooklm-adhd-notebook.zip)** (open it, then click the download button).
3. In Claude, open **Settings** → **Capabilities** → **Skills**, click **Upload skill**, and upload each file.

If you do not see Upload skill, turn on **Code execution** on the same screen first.

## Dependency on the ADHD plugin

Like two code packages: this plugin depends on **adhd-mode** and declares it in `plugin.json` (`"dependencies": ["adhd-mode@claude-code-adhd-assist"]`). `notebooklm-summary-adaptation` loads the ADHD rules from `adhd-mode:adhd-on` each time it runs, so when the ADHD plugin is updated, summaries follow the new rules with no change here. If the ADHD plugin is missing (possible only in the chat), `notebooklm-summary-adaptation` stops and links to it.

## How a study session goes

1. In NotebookLM: collect sources with **Deep Research**.
2. In the notebook's chat: ask for a summary of the sources.
3. In Claude: open a new chat and type `/notebooklm-summary-adaptation`.
4. Send the notebook link when asked. Claude opens it in Chrome, reads the summary and builds the adapted page.

If the notebook has no sources or no summary yet, Claude tells you which step is missing; do it and come back.

## Notes

- `notebooklm-summary-adaptation` always applies the ADHD rules to the summary page. Whether ADHD mode also turns on in the chat is your choice (see `/notebooklm-adhd-settings`).
- Where the choice is kept: in Claude Code, in `~/.claude/notebooklm-adhd-settings.json`. In the Claude chat, in Claude's memory when memory is on; otherwise you are asked again in each new chat.
- The zip holds the same files you see in this repository.

## Credits

The ADHD rules are adapted from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) (MIT License, see `LICENSE.txt`). Not made by Anthropic or Google. It changes how answers are formatted; it does not diagnose or treat anything.
