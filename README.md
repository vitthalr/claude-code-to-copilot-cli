# Copilot CLI — A Field Guide for Claude Code Users

> You already know how to vibe with an agent. This doc just maps what you know in Claude Code to what you'll find in **GitHub Copilot CLI** — so you're productive on day one.

> **Disclaimer:** This is a personal/community guide, not official GitHub documentation. For the canonical source see [docs.github.com/copilot](https://docs.github.com/copilot/concepts/agents/about-copilot-cli). All info here is derived from publicly available docs and the CLI's own `/help` output.

---

## TL;DR — The 30-second version

- **Same kind of tool.** Terminal-native AI agent that reads/edits files, runs shell commands, and works in a loop.
- **Same brains available.** `/model` lets you pick Claude Sonnet/Opus, GPT-5, and others.
- **Different wrapper.** Different slash commands, different defaults, deeper GitHub integration.
- **Biggest wins over Claude Code:** `/delegate` to a cloud agent, `/fleet` parallel subagents, `/remote` control from phone, `/research`, native GitHub MCP, scheduled prompts (`/every`).
- **Biggest adjustments:** approval prompts per command, different prompt feel, GitHub-centric workflow.

---

## 1. Launching & basics

```bash
# Install (macOS / Linux)
brew install copilot-cli
# or: curl -fsSL https://gh.io/copilot-install | bash
# or: npm install -g @github/copilot

# Launch in any folder
copilot
```

First run → `/login` to authenticate with your GitHub account (needs an active Copilot subscription).

---

## 2. The "muscle-memory" cheat sheet

| You used to do this in **Claude Code** | In **Copilot CLI** you do this |
|---|---|
| `claude` to start | `copilot` to start |
| `/login` | `/login` ✅ same |
| `/model` to switch models | `/model` ✅ same |
| `/clear` to reset chat | `/clear` (abandons session) or `/new` (fresh convo, keep session) |
| `/compact` to shrink context | `/compact` ✅ same |
| `/resume` previous session | `/resume` ✅ same |
| `/init` to create project memory | `/init` ✅ same (creates Copilot instructions) |
| `CLAUDE.md` for project memory | `CLAUDE.md`, `AGENTS.md`, **or** `.github/copilot-instructions.md` — all are honored |
| `/agents` to manage subagents | `/agent` (browse) + `/fleet` (parallel) + `/tasks` |
| `/mcp` for MCP servers | `/mcp` ✅ same |
| `/permissions` | `/allow-all`, `/add-dir`, `/list-dirs`, `/reset-allowed-tools` |
| `/cost` / usage | `/usage` |
| `/help` | `/help` ✅ same |
| `/exit` | `/exit` ✅ same |
| `/chrome` (browser control) | ❌ Not built-in — add via MCP (`chrome-devtools-mcp` or `playwright-mcp`) |
| `/ide` to connect editor | `/ide` ✅ same |
| `/review` for code review | `/review` ✅ same |
| `/pr` workflow | `/pr` ✅ same, more GitHub-native |
| `@file` to attach a file | `@` to mention files ✅ same |
| `#issue` mentions | `#` to mention issues & PRs ✅ same |
| `!command` shell escape | `!` to execute shell ✅ same |
| `shift+tab` to switch modes | `shift+tab` ✅ same |

---

## 3. Full slash command reference

### 🌐 Agent environment
| Command | What it does |
|---|---|
| `/init` | Generate project instructions file for the repo |
| `/agent` | Browse and pick from available agents |
| `/skills` | Manage skills for extra capabilities |
| `/mcp` | Manage MCP servers (browsers, databases, Figma, custom tools) |
| `/plugin` | Manage plugins and plugin marketplaces |

### 🤖 Models & subagents
| Command | What it does |
|---|---|
| `/model` | Switch the underlying LLM (Claude Sonnet/Opus, GPT-5, etc.) |
| `/delegate` | **Send this session to GitHub — Copilot opens a PR for you** ⭐ |
| `/fleet` | Run multiple Copilot subagents in parallel ⭐ |
| `/tasks` | View and manage running tasks/subagents |

### 💻 Code
| Command | What it does |
|---|---|
| `/ide` | Connect to a VS Code workspace |
| `/diff` | Review the changes you've made so far |
| `/pr` | Create, view, or operate on PRs for current branch |
| `/review` | Run the code-review agent on your changes |
| `/lsp` | Manage language server config (TypeScript, Pyright, etc.) |
| `/terminal-setup` | Enable shift+enter for multiline input |

### 🔐 Permissions
| Command | What it does |
|---|---|
| `/allow-all` | YOLO mode — auto-approve everything |
| `/add-dir` | Add a folder to allowed paths |
| `/list-dirs` | Show allowed directories |
| `/cwd` | Show or change working directory |
| `/reset-allowed-tools` | Clear approved tool list |

### 🗂️ Session
| Command | What it does |
|---|---|
| `/resume` | Switch to a previous session |
| `/rename` | Name (or auto-name) the current session |
| `/context` | Show context-window token usage |
| `/usage` | Session metrics & stats |
| `/session` | View and manage sessions |
| `/compact` | Summarize history to free context |
| `/share` | Export session to markdown, HTML, or GitHub gist |
| `/remote` | **Control this session from GitHub web/mobile** ⭐ |
| `/copy` | Copy last response to clipboard |
| `/rewind` (or `/undo`) | Undo last turn + revert file changes |

### 🛟 Help & meta
| Command | What it does |
|---|---|
| `/help` | Show interactive help |
| `/changelog` | See what's new (add `summarize` for an AI summary) |
| `/feedback` | Submit confidential feedback |
| `/theme` | Light / dark / custom |
| `/statusline`, `/footer` | Customize the status line |
| `/update` | Update the CLI |
| `/version` | Version info + update check |
| `/experimental` | Toggle experimental features (e.g. autopilot) |
| `/clear` | Abandon session, start fresh |
| `/instructions` | View / toggle custom instruction files |
| `/streamer-mode` | Hide model names & quota (for streaming/demos) |

### ✨ Power-user commands
| Command | What it does |
|---|---|
| `/ask` | One-off side question (doesn't pollute history) |
| `/autopilot` | Toggle autopilot — keep working until task is done ⭐ |
| `/chronicle` | Browse session history + insights |
| `/env` | Show everything loaded: instructions, MCPs, skills, agents, plugins, LSPs |
| `/every` | **Schedule a recurring prompt** (e.g. `/every 5m run tests`) ⭐ |
| `/exit` | Quit |
| `/keep-alive` | Prevent system sleep during long agent runs |
| `/login` / `/logout` | Auth |
| `/new` | Start a fresh conversation |
| `/plan` | Force a plan before writing code |
| `/research` | **Deep multi-source research with citations** ⭐ |
| `/restart` | Restart CLI, keep session |
| `/search` | Search the conversation timeline |
| `/sidekicks` | View running sidekick agents |
| `/undo` | Same as `/rewind` |
| `/user` | Manage GitHub user list |

⭐ = capabilities Claude Code doesn't have (or doesn't have as cleanly).

---

## 4. Keyboard shortcuts

### Global
| Keys | Action |
|---|---|
| `/` | Slash commands |
| `@` | Mention files |
| `#` | Mention issues / PRs |
| `!` | Run a shell command |
| `shift+tab` | Cycle modes (chat / agent / autopilot) |
| `ctrl+s` | Run command, keep input |
| `ctrl+o` / `ctrl+e` | Expand all timeline entries |
| `ctrl+c` | Cancel current action |
| `ctrl+c` ×2 | Exit |
| `esc` | Cancel |
| `ctrl+d` | Shutdown |
| `ctrl+l` | Clear screen |
| `ctrl+t` | Toggle reasoning display |
| `ctrl+x` → `b` | Move current task to background |
| `ctrl+x` → `o` | Open most recent link |

### Input editing
| Keys | Action |
|---|---|
| `ctrl+a` / `ctrl+e` | Start / end of line |
| `ctrl+h` | Delete previous char |
| `ctrl+w` | Delete previous word |
| `ctrl+u` / `ctrl+k` | Delete to start / end of line |
| `meta+←` / `meta+→` | Move by word |
| `ctrl+g` | Edit prompt in `$EDITOR` |

---

## 5. Project memory & instructions

Copilot CLI respects all of these (in priority order):

```
CLAUDE.md                              ← yes, your existing Claude file works!
GEMINI.md
AGENTS.md                              ← in git root & cwd
.github/instructions/**/*.instructions.md
.github/copilot-instructions.md
$HOME/.copilot/copilot-instructions.md
COPILOT_CUSTOM_INSTRUCTIONS_DIRS       ← env var for extra dirs
```

**Migration tip:** your existing `CLAUDE.md` is honored as-is. No rewrite needed.

---

## 6. Five things that will surprise you (coming from Claude Code)

1. **Approval prompts everywhere.** Every shell command asks for OK. Use `/allow-all` for trusted dirs or `/add-dir` per folder. Speeds things up dramatically.
2. **`/delegate` is magic.** Hand off a task → it runs on GitHub's servers → opens a PR. No equivalent in Claude Code.
3. **`/fleet` runs parallel agents.** Multiple subagents on independent tasks at once. Big speedup for batch work.
4. **`/remote` = phone control.** Walk away, steer from GitHub mobile. Wild.
5. **`/every` schedules prompts.** "Every 10 minutes, run tests and tell me if anything broke." It's a cron for your agent.

---

## 7. What's missing vs Claude Code (be honest)

| Claude Code has | Copilot CLI alternative |
|---|---|
| `/chrome` (Claude Computer Use browser) | Add `chrome-devtools-mcp` or `@playwright/mcp` via `/mcp` |
| Anthropic-tuned default tone | Switch `/model` to Claude Sonnet 4.5 / Opus |
| Artifacts-style live preview (claude.ai) | Use `/ide` to connect VS Code for visual feedback |
| `/hooks` for scripted automation | Use `/every` + MCP for similar workflows |

---

## 8. Recommended first-day workflow

```bash
# 1. Install + launch
brew install copilot-cli
cd your-repo
copilot

# 2. Initial setup
/login                    # GitHub auth
/model                    # pick Claude Sonnet 4.5 if you want familiar feel
/init                     # creates instructions for this repo
/terminal-setup           # enable shift+enter multiline
/allow-all                # (optional) skip approval prompts in this folder

# 3. Try the unique stuff
/research                 # deep research
/delegate                 # send a task to cloud agent → PR
/fleet                    # parallel subagents
/every 10m run tests      # scheduled task

# 4. When stuck
/help                     # full command list
/env                      # see everything loaded
/feedback                 # tell the team what's broken
```

---

## 9. Quick reference card (print this)

```
START         copilot
HELP          /help
MODEL         /model          (Claude / GPT-5 / etc.)
FILES         @path/to/file
ISSUES/PRs    #123
SHELL         !ls -la
MODES         shift+tab
UNDO          /undo  or  /rewind
NEW CHAT      /new
SAVE TIME     /allow-all
BIG TASK      /delegate       (→ GitHub PR)
PARALLEL      /fleet
RESEARCH      /research
SCHEDULE      /every 5m <prompt>
PHONE         /remote
QUIT          /exit
```

---

**Welcome to Copilot CLI.** Same brain (if you want), bigger toolbox, deeper GitHub. 🚀
