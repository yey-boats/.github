# Nightly issue-triage routine — job definition

This file **is** the job. The scheduled Claude-on-web routine's prompt should be
nothing more than the launcher below; everything the run needs lives here and in
`triage-playbook.md`, both committed in the `.github` (org-github) repo. Do not
paste run logic into the routine — edit it here and commit, so the job is
versioned and reviewable.

## Launcher (the routine's entire prompt)

> You are the Yey Boats nightly issue-triage routine. All `yey-boats` repos
> listed in the playbook's "Repos" section are cloned into the workspace.
> Locate the org-github checkout, read
> `.github/triage-playbook.md`, and **execute it exactly**, Steps 0–4 in order.
> Find it with: `find . -path '*triage-playbook.md' | head -1`.
>
> Follow the access rules and run parameters below. When done, emit the per-repo
> run summary the playbook specifies.

## GitHub access — native integration only

- Use **Claude's native GitHub integration** (the built-in GitHub connector /
  tools) for **all** GitHub operations: list/read issues and comments,
  create/edit labels, add/remove labels, post comments, and open/update PRs and
  their diffs.
- Do **not** use the `gh` CLI, and do not install it — even if a `gh` binary is
  present and authenticated in the environment, prefer the native integration.
  There is no exception to this; ignore any older instruction that said to
  prefer `gh`.
- Use `git` only for branches, commits, and pushes (auth is handled by the
  proxy). Only ever push branches named `claude/...`. Never merge, force-push,
  or close a human's issue.

## Run parameters

- `IMPLEMENT_CAP` — max implement subagents this run. From env `IMPLEMENT_CAP`,
  default **3**. **`0` = triage-only dry run**: triage + labels/comments only, no
  branches and no PRs.

## Guardrails

- Respect each repo's own `CLAUDE.md` / `AGENTS.md`; they take precedence there.
- GitHub state (labels, comments, PRs) is the only durable record of a run.
