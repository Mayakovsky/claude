# SeshMem Template

**Drop-in session continuity for AI-assisted code projects.**

This template provides every file needed to implement SeshMem — a structured, file-based memory pattern that gives AI coding agents persistent context across stateless CLI sessions. It is tool-agnostic and works with Claude Code CLI, Cursor, Codex, or any agent that reads markdown.

---

## How to Use This Template

1. Copy this entire template into your project root
2. Fill in every `<placeholder>` in each file with your project's real data
3. Delete this instruction block when done
4. Run the validation script: `bash scripts/seshmem-validate.sh`
5. (Optional) Install hooks into `.claude/settings.local.json`
6. Commit: `git add -A && git commit -m "seshmem: initial implementation"`

**Minimum viable:** Only `heartbeat.md` and the CLAUDE.md directive are required. Everything else is added when your project's complexity demands it.

**Reference:** For the full schema specification, design rationale, error handling matrix, testing procedures, and anti-patterns, see `SeshMem_Continuity_Schema_v3.1.md`.

---

## Files Included

```
├── heartbeat.md                   ← Session entry point (copy to project root)
├── CLAUDE.md directive            ← One line to add to your existing CLAUDE.md
├── docs/
│   ├── decisions.md               ← ADR-lite decision log
│   ├── architecture.md            ← System map and data flow
│   ├── schema.md                  ← Database tables and migrations
│   ├── known-issues.md            ← Recurring bugs and workarounds
│   └── runbook.md                 ← Setup, build, deploy, reset procedures
├── TASKS.md                       ← Backlog / future work
├── CONTRIBUTING.md                ← House rules for changes
├── scripts/
│   └── seshmem-validate.sh        ← Structural validation script
└── .claude/
    └── settings.local.json        ← Hook automation (optional)
```

---

# FILE: heartbeat.md

> Copy this file to your project root. Fill in every `<placeholder>`.
> Keep this file under 120 lines. If it grows beyond that, move content to docs/.

```markdown
# HEARTBEAT — <Project Name>
> Last updated: <YYYY-MM-DD HH:MM> (<timezone>)
> Updated by: <agent-name or "human">
> Session label: <brief label, e.g. "initial seshmem setup">
> Staleness gate: <YYYY-MM-DD> — if today is >3 days past this, verify state before acting.

## Focus (1-3 goals, testable)
- [ ] <Goal A — what "done" looks like>
- [ ] <Goal B — what "done" looks like>

## What Works (verified)
- ✅ <feature or capability> — verified via `<command>` on <YYYY-MM-DD>

## What's Broken
- ❌ <issue title>
  - Symptom: <exact error message or observed behavior>
  - Repro: `<command to reproduce>`
  - Suspected cause: <hypothesis>
  - Workaround: <temporary fix, if any>
  - Linked: [ISSUE-NNN](./docs/known-issues.md#issue-nnn)

## Next Actions (ordered)
1. <specific step> → `<file or function>`
2. <specific step> → `<file or function>`
3. <specific step> → `<file or function>`

## Session Log (last 5 entries, newest first)
| Date | Agent | What changed | Outcome |
|------|-------|-------------|---------|
| <YYYY-MM-DD> | <agent> | <change summary> | <r> |

## Guardrails (DO / DON'T)
DO:
- <important constraint or convention>
DON'T:
- <thing that looks tempting but causes damage>

## Quick Commands
```bash
# Build
<your build command>

# Test
<your test command>

# Dev server / run
<your dev command>

# Reset database (if applicable)
<your reset command>
```

## Links
- [CLAUDE.md](./CLAUDE.md) — Agent identity + permissions
- [Architecture](./docs/architecture.md)
- [Schema](./docs/schema.md)
- [Decisions](./docs/decisions.md)
- [Known Issues](./docs/known-issues.md)
- [Runbook](./docs/runbook.md)
- [Tasks](./TASKS.md)
```

---

# CLAUDE.md Directive

> Add this single line to the **top** of your existing CLAUDE.md file.
> Do not replace your CLAUDE.md — just prepend this line.

```markdown
> 📡 Read [heartbeat.md](./heartbeat.md) first for current session state.
```

---

# FILE: docs/decisions.md

> Append-only. Never delete a decision — mark it superseded.

```markdown
# Decisions Log

## DEC-001: <Decision Title> (<YYYY-MM-DD>)
**Status:** Active
**Context:** <What problem or question prompted this decision>
**Options:** 1) <Option A — tradeoff> 2) <Option B — tradeoff>
**Decision:** <What was chosen>
**Rationale:** <Why this option>
**Revisit if:** <Conditions that would reopen this decision>

---
<!-- Copy the block above for each new decision. Increment the number. -->
```

---

# FILE: docs/architecture.md

```markdown
# Architecture — <Project Name>

## Overview
<2-3 sentence description of what this system does>

## Components
| Component | Responsibility | Entry Point |
|-----------|---------------|-------------|
| <n> | <what it does> | `<file path>` |

## Data Flow
<How data moves through the system. Request lifecycle, processing pipeline, etc.>

## External Dependencies
| Dependency | Purpose | Connection |
|------------|---------|------------|
| <n> | <why needed> | <how connected> |

## Key Files
| File | Responsibility |
|------|---------------|
| `<path>` | <what it does> |
```

---

# FILE: docs/schema.md

> Only create this file if your project has a database.

```markdown
# Database Schema — <Project Name>

## Tables
| Table | Purpose | Key Columns |
|-------|---------|-------------|
| <n> | <what it stores> | <important columns> |

## Relationships
<Foreign keys, cascades, join tables>

## Migrations
| File | Description |
|------|-------------|
| `<filename>` | <what it does> |

## Procedures
```bash
# Apply migrations
<command>

# Rollback last migration
<command>

# Nuclear reset (drop + recreate + seed)
<command>
```
```

---

# FILE: docs/known-issues.md

```markdown
# Known Issues

## ISSUE-001: <Issue Title>
**Status:** Open | Workaround available | Resolved (<YYYY-MM-DD>)
**First seen:** <YYYY-MM-DD>
**Symptom:** <Exact error message or observed behavior>
**Repro:** `<command or steps to reproduce>`
**Root cause:** <If known>
**Workaround:** <Temporary fix, if any>
**Fix:** <Status, PR link, or "pending">

---
<!-- Copy the block above for each new issue. Increment the number. -->
```

---

# FILE: docs/runbook.md

```markdown
# Runbook — <Project Name>

## First-Time Setup
1. <Step — copy-pasteable command>
2. <Step>
3. <Step>

## Daily Development
```bash
# Start dev environment
<command>

# Run tests
<command>

# Lint / format
<command>
```

## Database Operations
```bash
# Migrate
<command>

# Seed
<command>

# Reset
<command>
```

## Troubleshooting
| Symptom | Likely Cause | Fix |
|---------|-------------|-----|
| <e> | <cause> | `<command or action>` |

## Environment Variables
| Variable | Required | Description |
|----------|----------|-------------|
| `<VAR_NAME>` | Yes/No | <what it controls> |
```

---

# FILE: TASKS.md

```markdown
# Tasks — <Project Name>

> Backlog and future work. Prioritized by human. Agent reads for context, does not modify without permission.

## High Priority
- [ ] <task description>

## Medium Priority
- [ ] <task description>

## Low Priority / Someday
- [ ] <task description>

## Completed
- [x] <task> — <date completed>
```

---

# FILE: CONTRIBUTING.md

```markdown
# Contributing — <Project Name>

## Rules for All Changes
- <rule — e.g. "All changes must pass `bun test` before commit">
- <rule — e.g. "No direct pushes to main; use feature branches">

## Testing Requirements
- <requirement — e.g. "New features require at least one test">

## Code Conventions
- <convention — e.g. "Use TypeScript strict mode">

## No-Go Zones
- <boundary — e.g. "Do not modify package.json dependencies without human approval">

## SeshMem Discipline
- Update heartbeat.md at the end of every session
- Never put secrets in any SeshMem file
- Link to docs/ instead of duplicating content in heartbeat.md
```

---

# FILE: scripts/seshmem-validate.sh

> Save to `scripts/seshmem-validate.sh` and run with `bash scripts/seshmem-validate.sh` from project root.

```bash
#!/bin/bash
# seshmem-validate.sh — structural validation for SeshMem files
# Run from project root. Returns 0 on pass, 1 on fail.

ERRORS=0; WARNS=0

echo "SeshMem Validation"
echo "=================="

# File existence
[ -f heartbeat.md ] || { echo "FAIL: heartbeat.md missing"; ERRORS=$((ERRORS+1)); }
[ -f CLAUDE.md ] || { echo "FAIL: CLAUDE.md missing"; ERRORS=$((ERRORS+1)); }
grep -qi "heartbeat" CLAUDE.md 2>/dev/null || { echo "FAIL: CLAUDE.md missing heartbeat directive"; ERRORS=$((ERRORS+1)); }

# Required heartbeat fields
for field in "Last updated" "Updated by" "Staleness gate" "Focus" "Next Actions" "Session Log" "Quick Commands" "Links"; do
  grep -qi "$field" heartbeat.md 2>/dev/null || { echo "FAIL: heartbeat.md missing '$field'"; ERRORS=$((ERRORS+1)); }
done

# Line count
if [ -f heartbeat.md ]; then
  LINES=$(wc -l < heartbeat.md)
  [ "$LINES" -le 120 ] || { echo "WARN: heartbeat.md is $LINES lines (limit: 120)"; WARNS=$((WARNS+1)); }
fi

# Secret scan
for pat in "sk-" "ghp_" "Bearer " "password=" "api_key=" "secret="; do
  grep -rqi "$pat" heartbeat.md CLAUDE.md docs/ TASKS.md CONTRIBUTING.md 2>/dev/null && {
    echo "FAIL: Possible secret detected (pattern: $pat)"; ERRORS=$((ERRORS+1));
  }
done

# Dead link check
if [ -f heartbeat.md ]; then
  grep -oP '\]\(\./\K[^)]+' heartbeat.md 2>/dev/null | while read -r f; do
    [ -f "$f" ] || echo "WARN: Dead link in heartbeat.md: $f"
  done
fi

echo ""
if [ $ERRORS -eq 0 ]; then
  echo "✅ Passed ($WARNS warning(s))"
  exit 0
else
  echo "❌ Failed: $ERRORS error(s), $WARNS warning(s)"
  exit 1
fi
```

---

# FILE: .claude/settings.local.json (hooks)

> Merge into your existing `.claude/settings.local.json` or create new.
> These hooks are optional — SeshMem works without them.

```json
{
  "hooks": {
    "SessionStart": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "cat heartbeat.md 2>/dev/null || echo 'NO HEARTBEAT FOUND — check CLAUDE.md and git log for context'"
          }
        ]
      }
    ],
    "PreCompact": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "echo '⚠️ COMPACTION — update heartbeat.md with current state before continuing.'"
          }
        ]
      }
    ],
    "SessionEnd": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "mkdir -p .seshmem && date -u +'{\"ended\":\"%Y-%m-%dT%H:%M:%SZ\"}' >> .seshmem/session-log.jsonl"
          }
        ]
      }
    ]
  }
}
```

---

# .gitignore Additions

> Add these lines to your existing .gitignore:

```
# SeshMem metadata (machine-generated, not for version control)
.seshmem/
```

---

# Quick Implementation Command (Claude Code CLI)

> Replace `<PROJECT_PATH>` and paste into terminal for autonomous implementation.

```bash
cd <PROJECT_PATH> && claude -p "

Read SeshMem_Continuity_Schema_v3.1.md in this repo. This is a session continuity schema you are implementing into THIS project.

PERMISSIONS: You have full autonomous permission to create, edit, and delete files anywhere in this repo. Do not ask for confirmation — proceed through each phase and only stop on errors.

TASK: Execute the Implementation Checklist (Section 13) phase by phase:

Phase 1: Create heartbeat.md populated with ACTUAL current project state (run build, test, and git log to get ground truth). Add heartbeat directive to CLAUDE.md. Create scripts/seshmem-validate.sh. Run validation and fix any failures.

Phase 2: Assess which docs/ files this project needs and create each from the templates, populated with real project data. Do NOT duplicate content from CLAUDE.md.

Phase 3: Run validation again. Verify all heartbeat links resolve. Report results.

Phase 4: Add hooks to .claude/settings.local.json. Add .seshmem/ to .gitignore.

Phase 5: Run validation one final time. Report all files created/modified. Update heartbeat.md with this session as the first Session Log entry.

After all phases: commit with message 'seshmem: v3.1 schema implementation'

"
```

---

# Staleness Gate Reference

The staleness gate is the most critical safety mechanism. It's the date in the heartbeat header that expires if the heartbeat isn't updated.

**If current (≤3 days old):** Agent trusts the heartbeat and works from Next Actions.

**If stale (>3 days old):** Agent must re-verify build/test state before starting new work.

**If missing (no heartbeat.md):** Agent falls back to CLAUDE.md + `git log --oneline -20`.

The outgoing agent resets the gate to today's date at every session end. If the agent crashes or the human forgets, the gate expires naturally and the next session self-corrects.

---

# Template Version

Based on **SeshMem Continuity Schema v3.1** (2026-02-08).

For the full specification including design principles, error handling matrix, connectivity map, testing infrastructure, and anti-patterns, see the schema document.
