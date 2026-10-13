---
name: gh-tasks
description: "Use the GitHub CLI (gh) to perform GitHub tasks — repositories, issues, pull requests, gists, releases, and git operations. Activated only when the user message explicitly contains @gh. Use for listing/creating/getting issues and PRs, reviewing PRs, managing repositories, runs/CI, releases, and clones. Requires gh to be installed and authenticated (see Notes)."
user-invocable: true
license: MIT
compatibility: Designed for Kilo AI coding agents with the GitHub CLI (gh) installed and authenticated via `gh auth login`.
metadata:
  author: reak
  version: "1.0.0"
  openclaw:
    emoji: "🐙"
    homepage: https://dev.reak.in
    requires:
      bins:
        - gh
        - git
    install: []
allowed-tools: Bash(gh:*) Bash(git:*) Read Grep Glob
---

# gh Tasks

Use the GitHub CLI (`gh`) to perform real GitHub work on behalf of the user.
This skill is a task wrapper around `gh`, similar to how `@tod` wraps the TOD CLI.

## Mention Routing (STRICT)

Use `gh` **only** when the user message explicitly contains:

```
@gh
```

If the message does NOT contain `@gh`, do NOT use this skill. If both `@tod` and
`@gh` are mentioned, both may be used.

This routing is strict — never infer GitHub intent from context alone.

---

## Preconditions

Before doing any `gh` task, verify the tool is ready. If not, stop and tell the user
how to fix it (do not attempt an interactive `gh auth login`, which hangs without a
TTY):

```bash
gh auth status
```

- If `gh: command not found` -> tell the user to install gh into `~/bin` without sudo
  (download the official tarball from https://github.com/cli/cli/releases and copy
  `bin/gh`, then persist `export PATH="$HOME/bin:$PATH"`).
- If `You are not logged in` -> tell the user to authenticate with a token:
  `printf '%s' "$TOKEN" | gh auth login --with-token`
  (create a PAT at https://github.com/settings/tokens with `repo`, `read:org`,
  `gist` scopes).
- Always run from the repo working directory when a command needs repo context, or
  pass `-R owner/repo` explicitly.

---

## Common gh Commands

### Repositories

```bash
gh repo view                 # current repo
gh repo view owner/repo      # any repo
gh repo list                 # repos for current user / org
gh repo clone owner/repo     # clone
gh repo create               # create a new repo
gh repo fork owner/repo      # fork
```

### Issues

```bash
gh issue list
gh issue list --repo owner/repo --state open --label bug
gh issue get <number>
gh issue get <number> --comments
gh issue create --title "..." --body "..."
gh issue create --title "..." --body "..." --label bug --assignee @me
gh issue edit <number> --add-label "..." --state closed
gh issue close <number>
gh issue reopen <number>
```

### Pull Requests

```bash
gh pr list
gh pr list --repo owner/repo --state open
gh pr get <number>
gh pr get <number> --comments
gh pr get <number> --json reviews,statusCheckRollup   # CI + review status
gh pr create --title "..." --body "..." --base main
gh pr create --fill --web                             # fill from commits, open in browser
gh pr checkout <number>
gh pr diff <number>
gh pr review <number> --approve --body "..."
gh pr review <number> --request-changes --body "..."
gh pr merge <number> --squash --delete-branch
gh pr status                                            # your open PRs
```

### PR Review Workflow (recommended)

For every PR task, gather the same evidence you would in a real review:

1. `gh pr get <number>` — description, base/head, author.
2. `gh pr get <number> --json statusCheckRollup` — CI / checks status.
3. `gh pr get <number> --comments` — review discussion.
4. `gh pr get <number> --json reviews` — existing approvals / change requests.
5. `gh pr diff <number>` — the actual changes.

Always report: what changed, why, check status (success/failed/pending), review
status, and any unresolved discussion before approving or merging.

### CI / Actions

```bash
gh run list
gh run list --repo owner/repo --branch main
gh run view <run-id>
gh run view <run-id> --log-failed
gh workflow list
gh workflow run <name>
```

### Releases

```bash
gh release list
gh release view <tag>
gh release create <tag> --notes "..."
gh release create <tag> ./dist/* --title "..."
```

### Gists

```bash
gh gist create file.txt
gh gist list
gh gist view <id>
```

---

## Working Rules

- Prefer `--repo owner/repo` (`-R`) over `cd`-ing around, unless a git operation
  (clone/checkout/merge) genuinely needs the local repo.
- Use `--json` to get machine-readable output when you need to parse fields
  (reviews, checks, labels, assignees).
- Never hardcode a token. Auth is handled by `gh auth login` / OS keyring.
- Respect repo visibility: do not expose private repo contents unless the task
  requires it and the user is authorized.
- Batch independent `gh` lookups in parallel (multiple Bash calls in one message).

---

## Output Style

- Be factual and concise; summarize what was done and the outcome.
- Distinguish Facts (from `gh` output) from Actions taken.
- If a command fails, report the error and the likely fix rather than guessing.

## Notes

- `gh` must be installed and authenticated first. Setup (non-sudo) is out of scope
  here but summarized under Preconditions.
- Git operations that touch remotes use the protocol set by
  `gh config get git_protocol` (ssh or https).
