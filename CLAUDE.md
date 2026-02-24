# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Git-based interactive fiction project** (Git小説), not a software application. The repository tells a children's story ("子犬のおつかい" / "A Puppy's Errand") where:
- **story.md** is the narrative (written in hiragana-heavy, picture-book style, first-person "ぼく")
- **Git commit history** serves as a meta-narrative — an operations log from a higher-dimensional entity ("fate") manipulating the puppy's world
- Readers discover layered meaning by exploring commit history, branches, .gitignore, and file diffs

## Key Commands

There are no build/test/lint commands. The only operations are git commits following the 13-step procedure in `puppy-errand-instruction.md`.

Before every commit:
```bash
git config user.name "fate"
git config user.email "fate@unknown"
```

Branch merge must use `--no-ff` to preserve merge commits:
```bash
git merge --no-ff lost -m "merge: resolve lost state"
```

View the narrative structure:
```bash
git log --oneline --graph --all
```

## Architecture

The instruction file `puppy-errand-instruction.md` is the master spec defining all 13 commits.

**Files and their narrative roles:**

| File | Role |
|------|------|
| `story.md` | Main story text (modified across many commits) |
| `shopping-list.txt` | MacGuffin — stays empty until final commit 13, then contains mother's message |
| `weather.md` | World-state metadata (created at commit 3) |
| `distractions.md` | Hidden temptations (created at commit 8, then gitignored at commit 9) |
| `.gitignore` | Narrative device — "fate" censoring distractions from the reader's view |

**Commit message style:** English, lowercase, factual, no emotion. Pattern: `verb: description` (e.g., `init: create world`, `apply: rain to subject`, `error: shopping list data lost`).

**Branch structure:** A `lost` branch is created at commit 5 (puppy gets lost), receives commit 6 (cat NPC guides puppy), then merges back to main at commit 7 — representing a "branched world-line."

## Rules

- No `git rebase` or `git commit --amend` (history rewriting is forbidden)
- One commit = one operation, no mixing unrelated files
- Story text must be hiragana-heavy, picture-book tone
