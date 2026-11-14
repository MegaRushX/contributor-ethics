# Contribution Record

The public record of what we contributed and what happened. Merged, declined, and withdrawn entries are recorded with equal weight. A record that shows only merged work reads as a portfolio; the declined and withdrawn entries are the evidence that the charter means something.

Charter violations we find in our own conduct are recorded here too, with the correction.

## Entry format

```
### <date> — <project>
**Contribution:** <one line>
**PR:** <link>
**Outcome:** merged | declined | closed by us | withdrawn (AI policy) | pending
**Maintainer's stated reason:** <quote, if given. "None given" is a valid entry.>
**Charter version:** 1.0
**Disclosure used:** yes | no
**Tests run:** <what, where>
**Not tested:** <what>
**Notes:** <what we learned, what we'd do differently>
```

## Contributions to other projects

### 2026-11-12 — saltbo/zpan

**Contribution:** Moved the admin analytics page's hardcoded Chinese UI copy into `admin.analytics.*` locale keys (132 keys, en + zh), with locale tests and a no-CJK regression guard.
**PR:** https://github.com/saltbo/zpan/pull/595
**Outcome:** merged (`ecb38aec`)
**Maintainer's stated reason:** —
**Charter version:** predates v1.0
**Disclosure used:** **no** in the PR body. Added in the follow-up comment on 2026-11-13. See the self-review log below.
**Tests run:** frontend-unit suite (120 files, 3192 tests), typecheck, biome, spec/arch/http/changelog-i18n lints. Deployed preview verification, licensed certificate, and bilingual screenshots were run by the maintainers' own review agents — we asked them to do it because we had no Pro/Business license, and said so in the PR.
**Not tested:** we did not run the deployed preview ourselves; the E2E suite fails at the seed step on upstream main (known upstream blocker).
**Notes:** The project has no policy against AI-assisted contributions, and its maintainers review with their own agents. We followed the project's preview-verification gate by naming the gap in the PR rather than claiming a pass. Project rules outranked our convenience.

### 2026-11-11 — saltbo/zpan

**Contribution:** Pass a relative `callbackURL` for email verification links, with integration tests capturing the sent email link.
**PR:** https://github.com/saltbo/zpan/pull/593
**Outcome:** closed by us, in favour of the maintainer's #596. Our commit was retained, recorded as `Co-authored-by: xWaLeEdOoOx <k.tolbah@gmail.com>` in the squash.
**Maintainer's stated reason:** "Using a relative callback alone leaves `/%2Ffiles` intact. Better Auth rejects that relative value with `Invalid callbackURL`, so it can prevent verification-email resend." The fix was correct but incomplete: three route guards call `encodeURIComponent` before handing the continuation to TanStack Router, so the relative callback reaches the origin check as `/%2Ffiles/…` and returns 403 on pages reached through `/_authenticated`, `/oauth`, or `/store/checkout`. Merging #593 alone would have broken sign-in.
**Charter version:** predates v1.0
**Disclosure used:** yes (in the closing comment and the analysis comment).
**Tests run:** backend integration suite (92), frontend unit (71), typecheck, biome, arch/http/spec lints.
**Not tested:** the guard-interaction path. We traced the code; we did not reproduce the 403 the maintainer found.
**Notes:** **The most important entry in this record.** Our analysis of the encoding chain was right, and our fix was incomplete in a way we did not test for. The maintainer found the missing half, kept our commit, and published the reason. We closed our PR ourselves, in favour of theirs, and stated the deficiency in plain terms in the thread. We did not argue, re-submit, or reframe. R9.

### 2026-11-13 — saltbo/zpan

**Contribution:** Move `UpgradeHint`'s hardcoded English copy (12 feature labels, 3 default strings) into `admin.upgrade.*` locale keys, removing the `charAt(0).toUpperCase()` capitalization hack.
**PR:** https://github.com/saltbo/zpan/pull/613
**Outcome:** pending
**Charter version:** 1.0
**Disclosure used:** yes — in the PR body.
**Tests run:** `vitest run --project frontend-unit` (121 files, 3205 tests), typecheck, `vite build --mode node` with the new strings confirmed in the built bundle.
**Not tested:** E2E. Stated in the PR body, with the reason: the suite fails at the seed step on upstream main (`BetterAuthError: The field "issuer" does not exist in the "account" Drizzle schema`), which is upstream, not this change.
**Notes:** One focused PR, 53 additions / 25 deletions, 4 files. No drive-by changes. We checked open issues and open PRs before posting, as we told the maintainer we would.

## Contributions to our own repositories

These are our own projects, not contributions to someone else's roadmap, so they are recorded for completeness rather than as charter evidence.

| Date | Repo | PR | Outcome |
| --- | --- | --- | --- |
| 2026-11-03 | xWaLeEdOoOx/skin-smith | #2 — v0.8.4, Theme Manager, admin-gate hardening, UI/UX overhaul | merged |
| 2026-11-03 | xWaLeEdOoOx/skin-smith | #3 — READMEs point at GitHub Releases | merged |
| 2026-11-05 | xWaLeEdOoOx/skin-smith | #5 — scope custom CSS exactly as TDP does | merged |
| 2026-11-05 | xWaLeEdOoOx/skin-smith | #7 — Contributor Covenant Code of Conduct | merged |

## Self-review log

### 2026-11-12 — Charter rule R3

**What happened:** PR #595 to saltbo/zpan was submitted without the AI disclosure block in the body. The work was disclosed in a follow-up comment the next day, not at submission.
**How it was found:** self-review against R3 when this charter was published.
**Correction:** R3 requires the disclosure block in the submission itself. PR #613 (2026-11-13) complies, and every submission from here on carries the block in the body and as a commit trailer.
**Public:** recorded here, not edited out. This entry predates the charter's publication, so the rule did not yet bind us. It binds us now, and this entry is where the gap is stated.
