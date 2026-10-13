---
name: standup-report
description: "Generate a standup report from OneDev activity for the current user. Queries PRs and issues with yesterday's activity, formats them into a concise standup update with yesterday's work, today's plan, and blockers. Use when the user asks for a standup report, daily update, or status summary."
user-invocable: true
license: MIT
compatibility: Designed for Kilo AI coding agents with OneDev/TOD CLI access.
metadata:
  author: reak
  version: "1.0.0"
  openclaw:
    emoji: "📋"
    homepage: https://dev.reak.in
    requires:
      bins:
        - tod
    install: []
allowed-tools: Bash(tod:*) Bash(git:*) Read Grep Glob
---

# Standup Report

Generate a concise standup report by querying OneDev for the current user's recent activity.

## Workflow

1. **Determine current user**
   - Run `tod get-login-name` to get the OneDev login name.

2. **Determine yesterday's date**
   - Use the current date from the environment. Yesterday is `current date - 1 day`.
   - Format dates as `YYYY-MM-DD` for TOD queries.

3. **Query yesterday's activity**
   Run these TOD queries in parallel:
   - `tod pr list --query 'submitted by "<login>" and "Last Activity Date" is since "<yesterday>"' --count 50`
   - `tod issue list --query '"Assignees" is "<login>" and "Last Activity Date" is since "<yesterday>"' --count 50`
   - `tod pr list --query 'commented by "<login>" and "Last Activity Date" is since "<yesterday>"' --count 50`
   - `tod issue list --query 'commented by "<login>" and "Last Activity Date" is since "<yesterday>"' --count 50`

   Also fetch linked issues for active PRs:
   - For each active PR, run `tod pr get <pr-number>` to read the description and linked issues.

4. **Query today's plan**
   Run these TOD queries in parallel:
   - `tod pr list --query 'submitted by "<login>" and status is open' --count 50`
   - `tod issue list --query '"Assignees" is "<login>" and "State" is not "Closed"' --count 50`

5. **Identify blockers**
   Check for:
   - Issues in `In Progress` or `Testing` state with no recent movement
   - PRs with `has pending reviews` or `has unsuccessful builds`
   - Any issue/PR description mentioning "blocker", "blocked", "waiting", or "dependencies"

6. **Format the report**
   Use the following template:

   ```
   *YESTERDAY*

   [ ITEM_URL ]
   Brief description of what was worked on.

   [ ITEM_URL ]
   Brief description of investigation or work done.

   *TODAY*

   [ ITEM_URL ]
   Plan for today (continue, review, merge, etc.)

   [ ITEM_URL ]
   Plan for today (implement, test, verify, etc.)

   [BLOCKER] {participant} needs to provide X / waiting on Y
   ```

   Rules:
   - Use the real working URL from the TOD response `link` field as the header, wrapped in `[ ... ]` (e.g., `[ https://dev.reak.in/REAK/Apps/cobra-go/app/~issues/48 ]`).
   - Put the description on the next line, below the link header.
   - Never invent or hand-build URLs. Always copy the exact `link` value returned by TOD for that PR or issue.
   - Keep descriptions to 1-2 sentences max
   - If no PR exists for an issue, use the issue's `link`
   - Group related work under the same PR/issue if needed
   - Omit the BLOCKER section entirely if there are no blockers
   - If a PR is linked to an issue, mention the issue number in the description

7. **Output**
   - Return only the formatted markdown report
   - Do not include raw JSON or TOD output
   - Do not include explanations or conversational filler

  8. **Save the report to a dated file**
    - Ensure the directory `/home/reak/Documents/dev-reports/` exists using the `filesystem_create_directory` tool.
    - Save the generated report to `/home/reak/Documents/dev-reports/standup-<today>.md` using the `filesystem_write_file` tool.
    - Write the exact same markdown that was returned to the user.
    - After saving, mention the file path so the user knows where it was stored.

## Example Output

```markdown
*YESTERDAY*

[ https://dev.reak.in/REAK/Internal/ReceptionMonk/mobile-app/~issues/45 ]
Resolved the merge conflicts and fixed the UI issues introduced after merging with the dev branch. Completed the merge successfully.

[ https://dev.reak.in/REAK/Internal/ReceptionMonk/mobile-app/~issues/48 ]
Started working on UI improvements and completed the fixes for image and video messages.

*TODAY*

[ https://dev.reak.in/REAK/Internal/ReceptionMonk/mobile-app/~issues/48 ]
Continue working on the remaining UI improvements for audio and document messages and will complete this task.

[BLOCKER] {@dheeraj.jaiswal} needs to complete admin UI review for shadowban toggle
```

## Notes

- If TOD returns no results for a query, retry once with explicit `--project` flag using the project from a successful query.
- Do not inspect local git history or branches for standup content. OneDev is the source of truth.
- If the user has no activity yesterday, state that clearly and suggest checking for missed updates.
- Every report entry MUST use the exact `link` URL returned by TOD. Never fabricate, guess, or construct links manually — copy them verbatim from the query output.
