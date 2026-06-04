# Copilot CLI — A Field Guide for Claude Code Users

> You already know how to work with an AI agent in the terminal. This guide simply maps what you know from **Claude Code** to what you'll find in **GitHub Copilot CLI** — so you're productive on day one. Every command below is read straight from the CLI itself, so you can trust it.

> **Disclaimer:** This is a personal/community guide, not official GitHub documentation. For the canonical source see [docs.github.com/copilot](https://docs.github.com/copilot/concepts/agents/about-copilot-cli). Command descriptions are taken verbatim from the CLI's own command list (v1.0.59).

---

## Why Copilot CLI (the 30-second pitch)

- **Same kind of tool.** A terminal-native AI agent that reads and edits your files, runs shell commands, and works in a loop until the job is done.
- **Same brains, your choice.** `/model` lets you pick Claude Sonnet/Opus, GPT-5, Gemini, and more — all in one place.
- **Deeper GitHub power.** Hand a whole task to the cloud and get a pull request back (`/delegate`), run many agents at once (`/fleet`), steer it from your phone (`/remote`), and do real research with citations (`/research`).
- **It schedules work for you.** `/every` and `/after` let your agent run tasks on a timer — like an alarm clock for your code.
- **It checks its own work.** `/rubber-duck` gets a second opinion, `/security-review` hunts for vulnerabilities, and `/review` does code review.

In short: **same brain if you want it, a much bigger toolbox, and tighter GitHub integration.**

---

## If you remember only 10 things

You do **not** need to memorize the big table below. For vibe-coding, these 10 moves are enough — everything else is bonus power you can grow into:

| # | Do this | What it's for |
|---|---|---|
| 1 | `copilot` | Start it in any folder |
| 2 | `/model` | Pick your AI brain (Claude, GPT-5, Gemini…) |
| 3 | `@file` | Show it a file |
| 4 | `!command` | Run a terminal command |
| 5 | `/init` | Teach it your project's "house rules" |
| 6 | `/diff` | See what changed |
| 7 | `/undo` (or `/rewind`) | Take back the last step |
| 8 | `/compact` | Shrink a long chat to stay fast |
| 9 | `/resume` | Jump back into an earlier chat |
| 10 | `/help` | See everything |

> 📋 **A note on availability:** Copilot CLI is rolling out fast. Some commands sit behind feature flags, account entitlements, or your organization's policy. **If a command below doesn't appear in your `/help`, you're not doing anything wrong** — it just may not be switched on for your account yet. The 10 moves above work for everyone.

---

## 1. Claude Code → Copilot CLI: what's the difference?

If your fingers already know Claude Code, here's the quick translation. Most things are the same; a few have new names.

| You used to do this in **Claude Code** | In **Copilot CLI** you do this |
|---|---|
| `claude` to start | `copilot` to start |
| `/login` | `/login` ✅ same |
| `/model` to switch models | `/model` ✅ same |
| `/clear` to reset chat | `/clear` (abandons the session) or `/new` (fresh chat, keeps the session) |
| `/compact` to shrink context | `/compact` ✅ same |
| `/resume` a previous session | `/resume` ✅ same |
| `/init` to create project memory | `/init` ✅ same (creates Copilot instructions) |
| `CLAUDE.md` for project memory | `CLAUDE.md`, `AGENTS.md`, **or** `.github/copilot-instructions.md` — all are honored |
| `/agents` to manage subagents | `/agent` (browse) + `/fleet` (parallel) + `/tasks` (manage) |
| `/mcp` for MCP servers | `/mcp` ✅ same |
| `/permissions` | `/allow-all`, `/add-dir`, `/list-dirs`, `/reset-allowed-tools` |
| `/cost` / usage | `/usage` |
| `/help` | `/help` ✅ same |
| `/exit` | `/exit` ✅ same |
| `/chrome` (browser control) | ❌ Not built-in — add it through `/mcp` (e.g. `chrome-devtools-mcp` or `playwright-mcp`) |
| `/ide` to connect your editor | `/ide` ✅ same |
| `/review` for code review | `/review` ✅ same |
| `/pr` workflow | `/pr` ✅ same, more GitHub-native |
| `@file` to attach a file | `@` to mention files ✅ same |
| `#issue` mentions | `#` to mention issues & PRs ✅ same |
| `!command` shell escape | `!` to run a shell command ✅ same |
| `shift+tab` to switch modes | `shift+tab` ✅ same |

**Migration tip:** your existing `CLAUDE.md` works as-is. No rewrite needed.

---

## 2. Every slash command, explained simply

> **How to read this table:** The middle column is the **exact words Copilot shows you** when you type `/`. The right column is the same idea **in plain English**, with an example of how to type it. Some commands take extra input (shown in `< >`) — just type the command, a space, then your text.

> 👤 **Designers / vibe-coders, relax:** anything tagged **🔧** is engineer-focused setup or plumbing. It's nice to know it exists, but **you don't need it to vibe-code** — feel free to skip those rows. Everything else is useful to know, though your exact `/help` list can vary by account, rollout, and organization policy. A **⚠️** means the command is **internal or still rolling out**, so it may not show up for you yet.

### 🌐 Set up your agent's environment
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/init` | Initialize Copilot instructions for this repository | Creates a "house rules" file so Copilot remembers how your project works. *Just type `/init` once per project.* |
| `/agent` | Browse and select from available agents (if any) | Picks a specialist helper (a custom agent) for the job. *Type `/agent` and choose from the list.* |
| `/skills` | Manage skills for enhanced capabilities | Turns extra abilities on or off (like add-on powers). *Type `/skills list` to see them.* |
| `/mcp` | Manage MCP server configuration | Connects outside tools — browsers, databases, Figma, etc. *Type `/mcp list` to see what's connected.* |
| `/plugin` | Manage plugins and plugin marketplaces | Installs bundles of extra features from a store. *Type `/plugin list`.* |

### 🤖 Pick a brain & run helpers
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/model` | Select AI model to use | Choose which AI brain runs — Claude, GPT-5, Gemini, etc. **Auto** lets Copilot pick for you, and one model is marked **(default)**. *Type `/model` and pick one.* ⭐ |
| `/delegate` | Send this session to GitHub and Copilot will create a PR | Hand the whole task to GitHub's cloud; it does the work and opens a pull request for you. *Needs a GitHub repo. Type `/delegate`.* ⭐ |
| `/fleet` | Enable fleet mode for parallel subagent execution | Runs several helper agents at the same time, so big jobs finish faster. *Type `/fleet` then describe the work.* ⭐ |
| `/autopilot` ⚠️ | Toggle autopilot mode or set an explicit objective | Lets Copilot keep going on its own until the goal is met. *Type `/autopilot` to turn on, or `/autopilot fix all failing tests`. ⚠️ Experimental — may be rolling out.* ⭐ |
| `/tasks` | View and manage tasks (subagents and shell commands) | A dashboard of everything currently running. *Type `/tasks`.* |
| `/rubber-duck` ⚠️ | Get an independent critique of your current work from the rubber duck agent | Asks a second AI to double-check the plan and catch mistakes. *Type `/rubber-duck` (optionally add a question). ⚠️ Rolling out — may not appear yet.* ⭐ |

### 💻 Write & review code
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/ide` | Connect to an IDE workspace | Links Copilot to your VS Code window so they share the same files. *Type `/ide`.* |
| `/diff` | Review the changes made in the current directory | Shows exactly what was changed, line by line. *Type `/diff`.* |
| `/pr` 🔧 | Operate on pull requests for the current branch | Create, view, or work on a GitHub pull request. *Type `/pr`.* |
| `/review` | Run code review agent to analyze changes | A robot reviewer reads your changes and flags real problems. *Type `/review`.* ⭐ |
| `/security-review` 🔧 | Analyze staged and unstaged changes for security vulnerabilities. | Scans your changes for security holes before you ship. *Type `/security-review`.* ⭐ |
| `/lsp` 🔧 | Manage language server configuration | Controls the "spell-checker for code" (TypeScript, Python, etc.). *Type `/lsp`.* |
| `/plan` | Create an implementation plan before coding | Makes a step-by-step plan first, then codes. *Type `/plan build a login page`.* |
| `/terminal-setup` 🔧 | Configure terminal for multiline input support (shift+enter) | One-time setup so `shift+enter` makes a new line. *Type `/terminal-setup` once.* |

### 🔐 Permissions & safety
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/allow-all` | Enable all permissions (tools, paths, and URLs) | Stops asking "is this OK?" for everything — fast, but **only use it in folders you trust** (it can run any command). *Type `/allow-all`.* |
| `/add-dir` 🔧 | Add a directory to the allowed list for file access | Lets Copilot touch one extra folder. *Type `/add-dir ./my-folder`.* |
| `/list-dirs` 🔧 | Display all allowed directories for file access | Shows which folders Copilot is allowed to use. *Type `/list-dirs`.* |
| `/cwd` 🔧 | Change working directory or show current directory | Shows or changes the folder you're working in. *Type `/cwd` to see it, or `/cwd ./project` to move.* |
| `/reset-allowed-tools` 🔧 | Reset the list of allowed tools | Forgets all the "yes, allow" answers and starts fresh. *Type `/reset-allowed-tools`.* |
| `/sandbox` 🔧 | Configure sandbox modes | Runs things in a safe, walled-off space. *Type `/sandbox enable`.* |

### 🗂️ Manage your session
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/resume` | Switch to a different session (optionally specify session ID, task ID, or name) | Re-opens an earlier conversation. *Type `/resume`.* |
| `/rename` | Rename the current session | Gives this chat a memorable name. *Type `/rename demo-prep`.* |
| `/context` | Show context window token usage and visualization | Shows how "full" the AI's memory is right now. *Type `/context`.* |
| `/usage` | Display session usage metrics and statistics | Shows how much you've used this session. *Type `/usage`.* |
| `/session` | View and manage sessions. Use subcommands for details. | Inspect or organize your sessions. *Type `/session info`.* |
| `/compact` | Summarize conversation history to reduce context window usage. Optionally provide focus instructions. | Shrinks a long chat into a summary to free up memory. *Type `/compact`, or `/compact keep the auth details`.* |
| `/share` | Share session or research report to markdown file, HTML file, or GitHub gist | Saves the conversation as a file or link you can send. *Type `/share`.* |
| `/remote` | Show remote status or toggle remote control from GitHub web and mobile | Lets you steer this session from your phone or the web. *Type `/remote on`.* ⭐ |
| `/copy` | Copy the last response to the clipboard | Copies the last answer so you can paste it. *Type `/copy`.* |
| `/rewind` | Rewind the last turn and revert file changes | Undo button — takes back the last step and its file edits. *Type `/rewind`.* |
| `/undo` | Rewind the last turn and revert file changes | Same as `/rewind`. *Type `/undo`.* |

### ⏰ Memory & scheduling (the "set it and forget it" powers)
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/every` | Schedule a recurring prompt or skill for this session | A repeating timer for your agent. Interval looks like `30s`, `5m`, `2h`, `1d`. *Example: `/every 10m run the tests and tell me if anything broke`.* ⭐ |
| `/after` | Schedule a one-shot prompt or skill for this session | A one-time delayed task. *Example: `/after 30m remind me to push my code`.* ⭐ |
| `/memory` | Show memory status, or enable/disable memory across sessions | Lets Copilot remember things between sessions. *Type `/memory show`, or `/memory on`.* |
| `/subconscious` 🔧 ⚠️ | Manage Copilot Subconscious memory consolidation | Tidies up long-term memory in the background. *Type `/subconscious run`. ⚠️ Experimental — may be rolling out.* |
| `/keep-alive` | Manage keep-alive mode (prevents system sleep). | Stops your Mac from sleeping during a long job. *Type `/keep-alive`.* |
| `/chronicle` | Session history tools and insights | Browse your past sessions and patterns. *Type `/chronicle`.* |

### 🔎 Research, search & ask
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/research` | Run deep research investigation using GitHub search and web sources | Does deep homework across GitHub and the web, with sources. *Type `/research best way to cache in Redis`.* ⭐ |
| `/ask` | Ask a quick side question without adding to conversation history | A quick side question that won't clutter the main chat. *Type `/ask what does this error mean?`* |
| `/search` | Search the conversation timeline | Find something said earlier in this chat. *Type `/search database`.* |

### 🎙️ Voice, help & settings
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/voice` | Manage voice mode (dictation transcription via Foundry Local) | Talk instead of type — your speech becomes text **on your own device** (private). *First use downloads a model; pick the larger one for fewer errors.* |
| `/help` | Show help for interactive commands | The full command list. *Type `/help`.* |
| `/changelog` | Display changelog for CLI versions. Add 'summarize' to get an AI summary. | See what's new in each version. *Type `/changelog`, or `/changelog summarize`.* |
| `/feedback` | Provide feedback about the CLI | Tell the GitHub team what's good or broken. *Type `/feedback`.* |
| `/theme` | View or set color mode | Switch colors (light/dark/custom). *Type `/theme`.* |
| `/statusline` | Configure status line items | Customize the info bar at the bottom. *Type `/statusline`.* |
| `/footer` | Configure status line items | Customize the footer bar. *Type `/footer`.* |
| `/streamer-mode` ⚠️ | Toggle streamer mode (hides preview model names and quota details for streaming) | Hides private details when screen-sharing — your **quota %** in the footer, and **preview model names** (in the `/model` list they show as *"Hidden Model 1, 2, 3…"*). *Turn it ON before you present. ⚠️ Internal/staff-only — may not appear on every account.* |
| `/instructions` 🔧 | View and toggle custom instruction files | See and switch which "house rules" files are active. *Type `/instructions`.* |
| `/env` 🔧 | Show loaded environment details (instructions, MCP servers, skills, agents, plugins, LSPs, extensions) | One screen showing everything that's loaded. *Type `/env`.* |
| `/experimental` 🔧 | Show available experimental features, or enable/disable experimental mode | Turn on early, in-progress features. *Type `/experimental`.* |

### ⚙️ Account & app control
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/login` | Log in to Copilot | Sign in with your GitHub account. *Type `/login`.* |
| `/logout` | Log out of an OAuth login session | Sign out. *Type `/logout`.* |
| `/user` | Manage GitHub user list | Switch between GitHub accounts. *Type `/user`.* |
| `/new` | Start a new conversation | Fresh chat, same session. *Type `/new`.* |
| `/clear` | Abandon this session and start fresh | Throw away this session and start over. *Type `/clear`.* |
| `/restart` | Restart the CLI, preserving the current session | Reboot the app but keep your work. *Type `/restart`.* |
| `/update` | Update the CLI to the latest version | Get the newest version. *Type `/update`.* |
| `/version` | Display version information and check for updates | Show which version you're on. *Type `/version`.* |
| `/exit` | Exit the CLI; use 'print' to print the session after exiting alt screen | Quit. *Type `/exit`.* |

⭐ = an especially useful Copilot CLI feature or workflow. (Availability may vary by account and rollout.)

---

## 3. Typing shortcuts (no slash needed)

These special keys work right in the prompt:

| Type this | What it does | In plain words |
|---|---|---|
| `@` | Mention files | Attach a file by name so Copilot can read it. |
| `#` | Mention issues and pull requests | Point Copilot at a GitHub issue or PR. |
| `!` | Execute shell command | Run a terminal command directly (e.g. `!ls -la`). |
| `/` | Commands | Opens the slash-command menu (everything above). |

---

## 4. Keyboard shortcuts

### Global
| Keys | Action |
|---|---|
| `shift+tab` | Switch modes (chat / agent / autopilot) |
| `ctrl+s` | Run command, keep your typed input |
| `ctrl+o` / `ctrl+e` | Expand all timeline entries |
| `ctrl+c` | Cancel the current action |
| `ctrl+c` ×2 | Exit |
| `esc` | Cancel |
| `ctrl+d` | Shutdown |
| `ctrl+l` | Clear the screen |
| `ctrl+t` | Toggle the reasoning display |
| `ctrl+x` → `b` | Move the current task to the background |
| `ctrl+x` → `o` | Open the most recent link |

### Editing your text
| Keys | Action |
|---|---|
| `ctrl+a` / `ctrl+e` | Jump to start / end of line |
| `ctrl+h` | Delete the previous character |
| `ctrl+w` | Delete the previous word |
| `ctrl+u` / `ctrl+k` | Delete to start / end of line |
| `meta+←` / `meta+→` | Move by word |
| `ctrl+g` | Edit your prompt in `$EDITOR` |

---

## 5. Project memory & instructions

Copilot CLI reads **all** of these files (the ones that exist), so it remembers how your project works:

```
CLAUDE.md                              ← your existing Claude file works as-is!
GEMINI.md
AGENTS.md                              ← in git root & current folder
.github/instructions/**/*.instructions.md
.github/copilot-instructions.md
$HOME/.copilot/copilot-instructions.md
COPILOT_CUSTOM_INSTRUCTIONS_DIRS       ← env var for extra folders
```

**Does it understand `CLAUDE.md`? Yes — no rename needed.** It's a built-in convention; Copilot CLI looks for `CLAUDE.md` automatically.

**Which one "wins" if I have several?** None — **they're merged, not ranked.** Copilot loads every file that exists and **combines them into one instruction set** (e.g. `CLAUDE.md` *plus* `AGENTS.md` *plus* `.github/copilot-instructions.md` are all honored together). So your old Claude setup keeps working, and you can layer Copilot-specific rules on top.

> ⚠️ **The one thing to avoid:** don't write **contradictory** rules in two different files. Since all of them reach the model, conflicting instructions confuse the *answer* — not the file-loading. Keep your rules consistent across files.

**Migration tip:** your existing `CLAUDE.md` is honored as-is. No rewrite needed.

---

## 6. Five things that will pleasantly surprise you

1. **It asks before acting.** Every shell command asks for an OK by default. Use `/allow-all` (or `/add-dir`) in folders you trust to speed things up.
2. **`/delegate` is magic when available.** In an eligible GitHub repo it hands the task to the cloud and opens a pull request for you.
3. **`/fleet` runs many agents at once.** Great for big, repetitive jobs.
4. **`/remote` = phone control.** Walk away and steer from GitHub mobile or web.
5. **`/every` and `/after` schedule work.** "Every 10 minutes, run the tests." It's a cron job for your agent.

---

## 7. Quick reference card (print this)

```
START          copilot
HELP           /help
PICK A BRAIN   /model            (Claude / GPT-5 / Gemini …)
ATTACH FILE    @path/to/file
ISSUE / PR     #123
RUN SHELL      !ls -la
SWITCH MODES   shift+tab
TALK TO IT     /voice
UNDO           /undo   or  /rewind
NEW CHAT       /new
TRUST A FOLDER /allow-all         (only in folders you trust!)
BIG TASK       /delegate         (→ GitHub PR)
MANY AT ONCE   /fleet
SECOND OPINION /rubber-duck
RESEARCH       /research <topic>
SCHEDULE       /every 10m <prompt>   ·   /after 30m <prompt>
PHONE CONTROL  /remote on
QUIT           /exit
```

---

**Welcome to Copilot CLI.** Same brain if you want it, a bigger toolbox, and deeper GitHub. 🚀
