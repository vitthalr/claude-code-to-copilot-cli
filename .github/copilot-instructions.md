# Copilot instructions for this repository

## What this repo is

A **documentation-only** repository. The single deliverable is `README.md` — a field
guide that maps **Anthropic Claude Code** concepts to **GitHub Copilot CLI** for an
audience of **designers who "vibe-code"** (non-engineers). There is no application code,
build, test suite, or linter. Changes are almost always edits to `README.md`.

## The most important rule: verify command facts against the CLI binary

Command names, descriptions, argument hints, and availability in `README.md` are **not**
guessed or taken from memory — they are extracted from the installed Copilot CLI binary,
which is the source of truth. When adding or changing any command claim, verify it:

- The binary lives at `~/.copilot/pkg/<platform>/<version>/app.js` (e.g.
  `~/.copilot/pkg/darwin-arm64/1.0.59/app.js`). It is minified JS; use `grep -oE` on it.
- **Exact descriptions** come from the `displayName:"/cmd",description:"..."` fields.
- **Argument hints / options** come from the `input:{hint:"..."}` and `choices:[...]` fields.
- **Availability** matters:
  - `staffOnly:true` commands (e.g. `/sidekicks`) are GitHub-internal — **omit them** from the doc.
  - Feature-gated commands default OFF and can throw `Unknown command` on normal accounts.
    These are gated in a central command-builder filter (e.g. `sandbox`, `security-review`,
    `subconscious`, `rubber-duck`, `every`, `after`). Tag them ⚠️.
  - To check what is actually enabled for the current account, look at
    `~/.copilot/command-history-state.json` (commands the user has really run).
- If the binary cannot be read (sandbox), fall back to the CLI's own `/help` output or
  official docs — but prefer the binary.

## README conventions (follow these exactly)

The main command reference is a 3-column table. Each row MUST keep this structure:

| Command | What Copilot shows you | In plain words (+ how to type it) |

- **Middle column** = the **exact** in-CLI description string (verbatim from the binary).
- **Right column** = plain-English explanation written for a 10th-grader, using an everyday
  analogy where helpful (e.g. sandbox = "play in this room, but the other doors are locked").
  Then a line break and an italic note listing options / how to type it.
- **Line breaks inside a cell** use a literal `<br>` before the italic options/how-to note,
  so the explanation and the note render on separate lines.
- **Per-option explanations**: when a command has sub-options, explain what each does inline,
  e.g. ``*Options: `on` (start remembering) · `off` (stop) · `show` (see what it knows).*``

### Icon legend (defined near the top of the command section)

- ⭐ = standout / "don't miss this" command.
- 🔧 = engineer/setup/plumbing — designers can skip it.
- ⚠️ = newer / rolling out — may show `Unknown command` if not enabled for the account.

Keep the **Legend** table and the **"If you remember only 10 things"** section in sync with
any command changes.

## Audience & tone

Write for **designers / vibe-coders**, not engineers. Avoid jargon; when a technical term is
unavoidable, immediately translate it with a simple analogy. Do not overwhelm — the full
command catalog is a reference, while the top-10 list is the thing people actually need.

## Editing workflow

- Edit `README.md` directly with surgical changes; preserve the table structure and icon tags.
- This is a public, community guide (not official GitHub docs) — keep the disclaimer intact.

## Git / commit notes

- The repo is pushed to `github.com/vitthalr/claude-code-to-copilot-cli` using the `vitthalr`
  GitHub account. Pushes use the gh credential helper:
  `git -c credential.helper='!gh auth git-credential' push origin main`.
- Use **single-line** commit messages — multi-line inline `-m` messages have hung the
  interactive shell in this environment.
