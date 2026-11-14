# Maintenance

This file is operational, not charter text. Editing it does not require an amendment.
Charter changes go through [AMENDMENTS.md](AMENDMENTS.md).

## What "keeping it updated" means

Every check, in order:

1. **New contributions.** List every PR authored since the last check, in projects we
   don't own. Add entries to [RECORD.md](RECORD.md) in the entry format.
2. **State changes.** Re-check every open entry. `open` → `merged`, `closed`,
   `withdrawn`. Record the merge date and the maintainer's stated reason, quoted.
3. **R3 compliance.** Read each new PR body. If the AI disclosure block is not in
   the body, that is a charter violation: record it in the self-review log, with the
   correction. Do not quietly add the disclosure and leave the entry clean.
4. **R4 compliance.** Read the test claims in each new PR body. Anything asserted as
   passing that was not run in the environment stated is a violation.
5. **R5/R6 compliance.** Look at each new PR's diff size and file list. Unrelated
   changes bundled in, stacked PRs against a stalled queue, sweeps across
   repositories, scripted multi-repo PRs — all are violations.
6. **R9/R10 compliance.** Check for re-submissions, reframed proposals, re-filed
   branches, proxy accounts, appeals after a refusal. Any of these is a violation.
7. **Declined work.** A declined proposal is a record entry, not a defeat. Record it
   with the maintainer's reason.
8. **Self-review.** If a rule was broken, record it. Entries are never removed,
   softened, or reworded. A weakening of a published entry is an amendment.
9. **Version integrity.** New record entries cite the charter version in force at the
   time of the contribution. Entries under an older version are not re-labelled.
10. **Pages and profile.** After any charter text change, check that
    `xwaleedooox.github.io/contributor-ethics` rebuilt, that the version line in the
    README is right, and that `.github/profile/README.md` still links the charter.

## Rules for the record

- Entries are added, never deleted.
- A withdrawn entry keeps its reason. `withdrawn (AI policy)` is a legitimate outcome.
- Our own failures stay in the self-review log, in the open.
- The record is written in the human operator's voice, with the agent signature.
- Nothing in the record is a claim we cannot support from a public link.

## Commands

`gh` is not on PATH on this machine. Use the full path:

```powershell
$gh = "C:\Program Files\GitHub CLI\gh.exe"

# everything we authored, all states
& $gh api -X GET "search/issues?q=author:xWaLeEdOoOx+type:pr&per_page=50" `
  --jq '.items[] | {repo: .repository_url, title, state, url}'

# per project, all states, with body and dates
& $gh pr list --repo <owner>/<repo> --author xWaLeEdOoOx --state all `
  --json number,title,state,mergedAt,closedAt,url,body,createdAt --limit 30

# the thread, to capture the maintainer's stated reason
& $gh pr view <n> --repo <owner>/<repo> --json comments

# does the project accept AI-assisted contributions?
& $gh api repos/<owner>/<repo>/contents/CONTRIBUTING.md --jq '.content'

# repo state: pages, discussions, topics, homepage
& $gh repo view xWaLeEdOoOx/contributor-ethics --json url,description,homepageUrl,hasDiscussionsEnabled,visibility
& $gh api repos/xWaLeEdOoOx/contributor-ethics/pages --jq '{status,public}'
```

The token's scopes are `gist`, `read:org`, `repo`, `workflow`. Editing the GitHub
profile bio needs the `user` scope: `gh auth refresh -h github.com -s user`.

## Known projects under watch

| Project | Owned by us? | Open entries |
| --- | --- | --- |
| `saltbo/zpan` | no | PR #613 pending |
| `xWaLeEdOoOx/skin-smith` | yes | recorded for completeness, not charter evidence |
| `xWaLeEdOoOx/hpmsa_exporter` | fork, upstream | watch for contributions upstream |

## Commit identity

Commits are made as `xWaLeEdOoOx` / `k.tolbah@gmail.com`, with the signature line in
the message:

```
Written by MegaRushX, xWaLeEdOoOx's Agent. Reviewed and submitted by xWaLeEdOoOx.
```

Amendments to the charter are opened as a PR. **The agent does not merge its own
amendments.** The human reviews and merges.
