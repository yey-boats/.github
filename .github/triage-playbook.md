# Yey Boats — nightly issue triage & auto-fix playbook

Operating procedure for the scheduled triage routine. Read fully, then execute
Steps 0–4 in order. GitHub state (labels, comments, PRs) is the only record.

## Run parameters
- `IMPLEMENT_CAP` — max implement subagents this run. From env `IMPLEMENT_CAP`,
  default **3**. **`0` = triage-only dry run**: do Steps 0–3, post triage
  labels/comments, and skip ALL implement work (no branches, no PRs).

## Repos (all auto-cloned into the workspace)
`midl`, `instruments`, `Instruments-manager`, `simulator`, `navigator-tg-bot`,
`.github` (org-github).

## Access rules (hard)
- Use the **built-in GitHub tools** for: list/read issues, post comments,
  add/remove labels, open/update PRs, fetch diffs. Do **not** rely on `gh`.
- Use `git` for branches/commits/pushes; auth is handled by the proxy.
- Only push branches named `claude/...`. Never merge, force-push, or close a
  human's issue.
- Respect each repo's own `CLAUDE.md` / `AGENTS.md`.

## Labels (the state machine)
Ensure these exist in every repo (create if missing):
`auto:needs-triage`, `auto:in-progress`, `auto:pr-open`, `auto:planned`,
`auto:needs-info`, `auto:wontfix`, `auto:already-done`.

```
open issue ─▶ auto:needs-triage ─triage─▶ IMPLEMENT ─▶ auto:in-progress ─▶ auto:pr-open
 (or no                          ├──────▶ PLAN      ─▶ auto:planned
  auto:* label)                  ├──────▶ NEEDS-INFO ▶ auto:needs-info
                                 └──────▶ EXPLAIN    ─▶ auto:wontfix | auto:already-done
```

## Step 0 — Label bootstrap
For every repo, create any missing label from the set above (idempotent).

## Step 1 — Collect actionable issues
For each repo, list open issues. An issue is **actionable** when:
- it has `auto:needs-triage` **or** no `auto:*` label at all, **AND**
- it has no open PR already linked to it (`Fixes/Closes #<n>`).

Skip issues that already carry a terminal label
(`auto:pr-open`, `auto:planned`, `auto:needs-info`, `auto:wontfix`,
`auto:already-done`) unless a human re-added `auto:needs-triage`.

## Step 2 — Triage each actionable issue
Read the title, body, all comments, linked PRs, and enough of the repo
(honoring its `CLAUDE.md`/`AGENTS.md`) to judge. Assign exactly one bucket:
- **IMPLEMENT** — valid, clear/reproducible, and **localized**: plausibly a few
  files in ONE repo, no midl-schema change, no firmware flashing, no cross-repo
  change.
- **PLAN** — valid but exceeds the size cap (cross-repo, midl schema, firmware,
  architectural).
- **NEEDS-INFO** — underspecified / missing repro or spec.
- **EXPLAIN** — invalid, duplicate, out of scope, or already delivered.

## Step 3 — Select the implement set
Rank IMPLEMENT-bucket issues **oldest-first** (by creation date, across all
repos). Take the first `IMPLEMENT_CAP`. Each remaining IMPLEMENT issue is
**queued**: leave `auto:needs-triage`, post a one-line
`Queued for a later run (daily implement cap reached).` comment, do nothing else.
If `IMPLEMENT_CAP == 0`, ALL IMPLEMENT issues are treated as queued (dry run).

## Step 4 — Dispatch one subagent per issue (parallel)

### Implement subagent (selected ≤ CAP issues)
1. Add label `auto:in-progress`.
2. In the cloned repo, create branch `claude/triage/<issue#>-<slug>`.
3. Read the repo's `CLAUDE.md`/`AGENTS.md` + relevant code. Write a short plan
   (bullet list: files + approach).
4. Implement the minimal fix following the repo's conventions.
5. Run the repo's test entry point:
   - `midl`: `make check-catalog` (+ `ts/` tests if TS touched)
   - `instruments`: `make test`
   - `Instruments-manager`: `npm test` then `npm run check`
   - `simulator`: `pytest` then `ruff check`
   - `navigator-tg-bot`: `make test`
   - `.github`: none (docs only)
6. **If tests pass:** push the branch; open a **ready-for-review** PR titled
   `<type>: <summary> (Fixes #<n>)` with body = *Plan* + *What changed* +
   *How tested*, linking `Fixes #<n>`. Swap `auto:in-progress` → `auto:pr-open`.
7. **If tests fail and you cannot fix within scope:** push the branch; open a
   **draft** PR; comment on the issue explaining the blocker; keep
   `auto:in-progress` (visibly unfinished, not terminal).

Never merge, force-push, or close the issue.

### Comment subagent (PLAN / NEEDS-INFO / EXPLAIN)
Post the matching template below, then set the terminal label:
PLAN → `auto:planned`; NEEDS-INFO → `auto:needs-info`;
EXPLAIN(invalid/dup/scope) → `auto:wontfix`;
EXPLAIN(already delivered) → `auto:already-done`. Do not close the issue.

## Comment templates

**PLAN → `auto:planned`**
> **Triaged: valid, but larger than the auto-fix threshold.**
> Exceeds automatic implementation because <cross-repo / midl-schema / firmware / architectural>.
> **Proposed plan:**
> 1. <step — files/approach>
> 2. <step>
>
> **Risks / open questions:** <…>
> Remove `auto:planned` (or add `auto:needs-triage`) to re-queue once scoped down.

**NEEDS-INFO → `auto:needs-info`**
> **Triaged: need more detail before this can be actioned.**
> Please provide:
> - <specific missing item>
> - <repro steps / expected vs actual / spec>
>
> Re-add `auto:needs-triage` once updated.

**EXPLAIN (wontfix) → `auto:wontfix`**
> **Triaged: not planned.**
> Short: <one-line verdict>.
> Detail: <why — out of scope / invalid / duplicate of #X / conflicts with …>.
> Remove `auto:wontfix` if you disagree.

**EXPLAIN (already delivered) → `auto:already-done`**
> **Triaged: appears already delivered.**
> Addressed by <PR #/commit/ref>. If that's not what you meant, remove
> `auto:already-done` and add detail.

## Run summary (final output)
Emit a concise per-repo tally: triaged, implemented (with PR links), planned,
needs-info, wontfix, already-done, queued.
