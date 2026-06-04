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

> 📋 **A quick note on availability.** Most commands work for everyone. A few newer ones are still rolling out, so they may not be switched on for every account yet. If you type a command tagged ⚠️ and see *"Unknown command,"* don't worry — it's not a mistake on your end, it just isn't enabled for you yet. Everything untagged works for everyone.

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

> 👤 **Designers / vibe-coders, relax:** anything tagged **🔧** is engineer-focused setup or plumbing. It's nice to know it exists, but **you don't need it to vibe-code** — feel free to skip those rows. Everything else is useful to know, though your exact `/help` list can vary by account, rollout, and organization policy.

**Legend — what the icons mean:**

| Icon | Meaning |
|---|---|
| ⭐ | **Star command** — an especially useful, "don't miss this" feature worth trying first. |
| 🔧 | **Engineer / setup** — plumbing for developers. Designers can safely skip these. |
| ⚠️ | **Newer / rolling out** — works on most accounts, but may show "Unknown command" if not yet enabled for yours. Not a bug. |

> **Tip on arguments:** most commands you just type on their own. Some accept extra input after the slash — type the command, a space, then your text or one of the options. Each command below spells out its options. (Intervals/delays look like `30s`, `5m`, `2h`, `1d`.)

### 🌐 Set up your agent's environment
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/init` | Initialize Copilot instructions for this repository | Creates a "house rules" file so Copilot remembers how your project works. <br>*Type `/init` once per project. Add `/init suppress` to do it quietly (it still writes the file, just without the chatty output).* |
| `/agent` | Browse and select from available agents (if any) | Picks a **specialist helper** for the job — like choosing the right expert from a list. <br>*Type `/agent` and choose one.* |
| `/skills` | Manage skills for enhanced capabilities | Turns extra abilities on or off (like add-on powers). <br>*Options: `list` (see all skills) · `info` (details of one) · `reload` (refresh after changes).* |
| `/mcp` | Manage MCP server configuration | Plugs **outside tools** into Copilot — like a browser, a database, or Figma. Think of it as adding new apps to your phone. <br>*Options: `list` (see connected tools) · `show` (details of one) · `enable` / `disable` (turn a tool on/off) · `reload` (refresh).* |
| `/plugin` | Manage plugins and plugin marketplaces | A **plugin is a bundle of extra features** you install from a store (a "marketplace"). <br>*Options: `list` (see installed plugins) · `marketplace add` / `remove` / `list` / `browse` (manage where plugins come from).* |

### 🤖 Pick a brain & run helpers
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/model` | Select AI model to use | Choose which AI brain runs — Claude, GPT-5, Gemini, etc. **Auto** lets Copilot pick for you, and one model is marked **(default)**. <br>*Type `/model` and pick one.* ⭐ |
| `/delegate` | Send this session to GitHub and Copilot will create a PR | **Hand the whole job to GitHub's cloud** — it does the work on its own computers and hands you back finished changes (a "pull request") to review. You don't have to babysit it. <br>*Needs a GitHub repo. Type `/delegate`.* ⭐ |
| `/fleet` | Enable fleet mode for parallel subagent execution | Puts **several helpers to work at the same time** instead of one, so big jobs finish faster — like a team splitting up chores. <br>*Type `/fleet` then describe the work.* ⭐ |
| `/autopilot` | Toggle autopilot mode or set an explicit objective | Lets Copilot keep working on its own until the goal is met. <br>*Options: `on` / `off` (turn it on or off) · or type a goal like `/autopilot fix all failing tests` (giving an explicit goal may be rolling out).* ⭐ |
| `/tasks` | View and manage tasks (subagents and shell commands) | A **dashboard of everything running right now** — background helpers and commands — so you can check on or stop them. <br>*Type `/tasks`.* |
| `/rubber-duck` | Get an independent critique of your current work from the rubber duck agent | Asks a **second, independent AI to double-check** the plan or work and catch mistakes you (or the first AI) might miss. Named after "rubber duck debugging." <br>*Type `/rubber-duck` (optionally add a question to focus on).* ⭐ |

### 💻 Write & review code
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/ide` | Connect to an IDE workspace | Links Copilot to your **code editor** (VS Code) so they share the same files and you see changes live. <br>*Type `/ide`.* |
| `/diff` | Review the changes made in the current directory | Shows **exactly what was changed**, line by line (added lines and removed lines), so you can see what the agent did before keeping it. <br>*Type `/diff`.* |
| `/pr` 🔧 | Operate on pull requests for the current branch | A **pull request (PR)** is how you propose your changes to be added to a project. This creates, views, or works on one. <br>*Type `/pr` (works when you're in a GitHub project).* |
| `/review` | Run code review agent to analyze changes | A **robot reviewer** reads through your changes and points out real problems — bugs, mistakes — before anyone else sees them. <br>*Type `/review` (optionally add what to focus on).* ⭐ |
| `/security-review` 🔧 | Analyze staged and unstaged changes for security vulnerabilities. | Scans your changes for security holes before you ship. <br>*Type `/security-review` (optionally add instructions).* ⭐ |
| `/lsp` 🔧 | Manage language server configuration | A **language server is a live code expert** for one language (like Python or TypeScript) — it lets Copilot jump to definitions, spot errors, and edit accurately, the way a code editor does. This manages those. <br>*Type `/lsp`.* |
| `/plan` | Create an implementation plan before coding | Asks Copilot to **make a step-by-step plan first**, so you can check the approach before it starts changing anything. <br>*Type `/plan` then what you want, e.g. `/plan build a login page`.* |
| `/terminal-setup` 🔧 | Configure terminal for multiline input support (shift+enter) | One-time setup so `shift+enter` makes a new line. <br>*Type `/terminal-setup` once.* |

### 🔐 Permissions & safety
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/allow-all` | Enable all permissions (tools, paths, and URLs) | Stops asking "is this OK?" for everything — fast, but **only use it in folders you trust** (it can run any command). <br>*Type `/allow-all`.* |
| `/add-dir` 🔧 | Add a directory to the allowed list for file access | Lets Copilot touch one extra folder. <br>*Type `/add-dir ./my-folder`.* |
| `/list-dirs` 🔧 | Display all allowed directories for file access | Shows which folders Copilot is allowed to use. <br>*Type `/list-dirs`.* |
| `/cwd` 🔧 | Change working directory or show current directory | Shows or changes the folder you're working in. <br>*Type `/cwd` to see it, or `/cwd ./project` to move.* |
| `/reset-allowed-tools` 🔧 | Reset the list of allowed tools | Forgets all the "yes, allow" answers and starts fresh. <br>*Type `/reset-allowed-tools`.* |
| `/sandbox` 🔧 | Configure sandbox modes | Puts a **safety wall** around the agent: it can work inside your project folder, but **can't touch the rest of your computer**. Like saying "you can play in this room, but the other doors are locked." <br>*Options: `enable` (wall on) · `disable` (wall off).* |

### 🗂️ Manage your session
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/resume` | Switch to a different session (optionally specify session ID, task ID, or name) | **Re-opens an earlier chat** so you can pick up where you left off. <br>*Type `/resume` and choose from the list, or add a name/ID.* |
| `/rename` | Rename the current session | Gives this chat a memorable name. <br>*Type `/rename demo-prep`.* |
| `/context` | Show context window token usage and visualization | Shows **how full the AI's short-term memory is** right now — like a battery bar for how much it can still keep in mind. <br>*Type `/context`.* |
| `/usage` | Display session usage metrics and statistics | Shows **how much you've used** in this chat (requests, etc.) — like checking your data usage. <br>*Type `/usage`.* |
| `/session` | View and manage sessions. Use subcommands for details. | Inspect or organize your chats. <br>*Options: `info` (this chat's details) · `checkpoints` (saved restore points) · `files` (files this chat touched) · `plan` (the current plan) · `rename` (give it a name).* |
| `/compact` | Summarize conversation history to reduce context window usage. Optionally provide focus instructions. | When a chat gets long and slow, this **shrinks it into a short summary** so the AI stays fast — like zipping a big file. <br>*Type `/compact`, or `/compact keep the login details`.* |
| `/share` | Share session or research report to markdown file, HTML file, or GitHub gist | **Saves this chat so you can send it to someone** — as a file or a shareable web link. <br>*Choose what: a `session` (this chat) or a `research` report. Choose the format: a Markdown file, an HTML file, or a GitHub gist (a quick shareable link).* |
| `/remote` | Show remote status or toggle remote control from GitHub web and mobile | Lets you steer this session from your phone or the web. <br>*Options: `on` (allow phone control) · `off` (stop it) · `show` (check status).* ⭐ |
| `/copy` | Copy the last response to the clipboard | Copies the last answer so you can paste it. <br>*Type `/copy`.* |
| `/rewind` | Rewind the last turn and revert file changes | Undo button — takes back the last step and its file edits. <br>*Type `/rewind`.* |
| `/undo` | Rewind the last turn and revert file changes | Same as `/rewind`. <br>*Type `/undo`.* |

### ⏰ Memory & scheduling (the "set it and forget it" powers)
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/every` | Schedule a recurring prompt or skill for this session | A repeating timer for your agent. Interval looks like `30s`, `5m`, `2h`, `1d`. <br>*Example: `/every 10m run the tests and tell me if anything broke`.* ⭐ |
| `/after` | Schedule a one-shot prompt or skill for this session | A one-time delayed task. <br>*Example: `/after 30m remind me to push my code`.* ⭐ |
| `/memory` | Show memory status, or enable/disable memory across sessions | Lets Copilot **remember useful facts about you and your work** between chats, so you don't repeat yourself. (It remembers facts, not whole conversations.) <br>*Options: `on` (start remembering) · `off` (stop) · `show` (see what it knows).* |
| `/subconscious` 🔧 ⚠️ | Manage Copilot Subconscious memory consolidation | **Tidies up what Copilot remembers** in the background — like your brain sorting memories while you sleep. <br>*Args: `run`. ⚠️ Currently gated off on many accounts — may show "Unknown command."* |
| `/keep-alive` | Manage keep-alive mode (prevents system sleep). | **Stops your Mac from going to sleep** during a long job, so the agent isn't interrupted when you step away. (Doesn't help if you close the lid.) <br>*Type `/keep-alive` to toggle it.* |
| `/chronicle` | Session history tools and insights | Looks back over your past chats and turns them into useful summaries. Like a diary that writes itself. <br>*Options: `standup` (what you got done, ready to share) · `tips` (personalized advice to use Copilot better) · `improve` (suggests fixes to your project's "house rules" file) · `cost-tips` (ways to use fewer tokens / save money) · `reindex` (rebuild the history if subcommands say "no sessions found").* |

### 🔎 Research, search & ask
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/research` | Run deep research investigation using GitHub search and web sources | Does deep homework across GitHub and the web, with sources. <br>*Type `/research best way to cache in Redis`.* ⭐ |
| `/ask` | Ask a quick side question without adding to conversation history | A quick side question that won't clutter the main chat. <br>*Type `/ask what does this error mean?`* |
| `/search` | Search the conversation timeline | **Find something said earlier** in this chat without scrolling. Like Ctrl+F for your conversation. <br>*Type `/search` then a word, e.g. `/search database`.* |

### 🎙️ Voice, help & settings
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/voice` | Manage voice mode (dictation transcription via Foundry Local) | Talk instead of type — your speech becomes text **on your own device** (private). <br>*First use downloads a model; pick the larger one for fewer errors.* |
| `/help` | Show help for interactive commands | The full command list. <br>*Type `/help`.* |
| `/changelog` | Display changelog for CLI versions. Add 'summarize' to get an AI summary. | **See what's new** in each version of Copilot CLI. <br>*Options: type `/changelog` for the list, or `/changelog summarize` to get a short AI summary instead of the raw notes.* |
| `/feedback` | Provide feedback about the CLI | Tell the GitHub team what's good or broken. <br>*Type `/feedback`.* |
| `/theme` | View or set color mode | **Changes the colors** of the CLI to suit your eyes or your room's lighting. <br>*Type `/theme` and pick light, dark, or a custom look.* |
| `/statusline` | Configure status line items | **Customizes the little info bar** so it shows the details you care about. <br>*Type `/statusline` to choose what appears.* |
| `/footer` | Configure status line items | Same idea as `/statusline` — **tweak what shows in the bottom bar**. <br>*Type `/footer`.* |
| `/streamer-mode` ⚠️ | Toggle streamer mode (hides preview model names and quota details for streaming) | **Hides private details when screen-sharing** — your **quota %** in the footer, and **preview model names** (in the `/model` list they show as *"Hidden Model 1, 2, 3…"*). <br>*Options: `on` (hide) · `off` (show again) · `models` (reveal just the model names). Turn it ON before you present. ⚠️ Internal/staff-only — may not appear on every account.* |
| `/instructions` 🔧 | View and toggle custom instruction files | Shows the **"house rules" files** Copilot is following, and lets you turn them on or off. <br>*Type `/instructions`.* |
| `/env` 🔧 | Show loaded environment details (instructions, MCP servers, skills, agents, plugins, LSPs, extensions) | **One screen showing everything that's currently loaded** — all your instructions, connected tools, skills, and plugins in one place. Great for "wait, what's switched on right now?" <br>*Type `/env`.* |
| `/experimental` 🔧 | Show available experimental features, or enable/disable experimental mode | Turn on early, in-progress features. <br>*Type `/experimental`.* |

### ⚙️ Account & app control
| Command | What Copilot shows you | In plain words (+ how to type it) |
|---|---|---|
| `/login` | Log in to Copilot | Sign in with your GitHub account. <br>*Type `/login`.* |
| `/logout` | Log out of an OAuth login session | Sign out. <br>*Type `/logout`.* |
| `/user` | Manage GitHub user list | **Switch between GitHub accounts** (handy if you have a work and a personal one). <br>*Options: `show` (current user) · `list` (all added users) · `switch` (change account).* |
| `/new` | Start a new conversation | Fresh chat, same session. <br>*Type `/new`.* |
| `/clear` | Abandon this session and start fresh | Throw away this session and start over. <br>*Type `/clear`.* |
| `/restart` | Restart the CLI, preserving the current session | Reboot the app but keep your work. <br>*Type `/restart`.* |
| `/update` | Update the CLI to the latest version | **Updates Copilot CLI itself** (runs `npm i -g @github/copilot`). <br>*Add `prerelease` to get early test versions. Note: this does NOT update your MCP servers, skills, or plugins — those are managed separately via `/mcp`, `/skills`, `/plugin`.* |
| `/version` | Display version information and check for updates | Show which version you're on. <br>*Type `/version`.* |
| `/exit` | Exit the CLI; use 'print' to print the session after exiting alt screen | **Quits Copilot CLI.** <br>*Type `/exit`. Add `print` (`/exit print`) to leave the conversation printed in your terminal instead of clearing the screen.* |

*(⭐ 🔧 ⚠️ — see the **Legend** at the top of this section.)*

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
