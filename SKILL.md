---
name: compliance-review
description: Review work for compliance with global CLAUDE.md and project-level rules before marking complete
---

# Compliance Review

Validate that completed work adheres to established engineering rules.

## Usage

Invoke at end of session or before marking work complete:

```
/compliance-review
```

Agent will:
1. Read global CLAUDE.md rules
2. Check project-level CLAUDE.md if exists
3. Review this conversation for compliance with:
   - **Git Discipline** — No monkeypatching, files staged immediately after creation/deletion
   - **Plan Mode** — Used for 3+ step tasks or architectural decisions
   - **Verification** — Work demonstrated/tested before completion
   - **Subagents** — File-heavy investigations delegated, not inline
   - **Documentation** — Docs updated when code changes
4. Report pass/fail with specific violations if any

## What to Check

**Git Discipline**
- Files staged with `git add` immediately after creation/deletion (check `git status` shows them staged)
- No monkeypatching (runtime module/class modifications). Refactors use DI, inheritance, or plugin pattern

**Plan Mode**
- Tasks 3+ steps or architectural decisions entered plan mode via EnterPlanMode
- Non-trivial changes justified with plan context

**Verification**
- Non-trivial edits followed by test runs, code execution, or live demo
- Conversation shows verification step before claiming "complete"

**Subagents**
- File-heavy investigations delegated to agents (Explore, general-purpose, agy:runner)
- Main thread didn't inline 3+ file reads for analysis

**Documentation**
- New modules or features include docstrings/comments where WHY is non-obvious
- README or docs updated when behavior changed
- Inline comments explain workarounds or constraints, not WHAT code does

## Notes

- Run before completing significant work
- Focuses on CLAUDE.md adherence, not code quality (separate tool: /code-review)
- Flag actual violations; respect intentional deferrals ("deferred Part 2 deliberately")
