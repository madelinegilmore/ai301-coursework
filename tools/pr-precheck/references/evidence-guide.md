# Evidence guide: where evidence lives in a PR package

An eval package is one markdown file with these sections, in order:
the header (`source:` and `captured:` lines), `## Repo facts`,
`## Issue`, `## Thread highlights`, `## Plan context`, and
`## Candidate PR` with its `### Title`, `### Description`,
`### Commits`, `### Diff`, and `### Test evidence` subsections. Grade
from the `.md` file; the `.json` twin holds the same content for the
harness. The `source:` line names the real issue but is not a link:
never open it. When anything outside the package disagrees with it,
the package wins.

In live mode the same parts come from these places:

| Package part | Live source |
|---|---|
| Plan context | `plan.md` in the working copy, including its Deviations section; on the house chain, the house plan and house repro pack |
| Title, Description | `pr_draft.md` |
| Commits | `git log --oneline main..HEAD` |
| Diff | `git diff main...HEAD` (three dots), plus `git diff --stat main...HEAD` for the file list |
| Test evidence | `test_evidence.md` |
| Repo facts | `.github/PULL_REQUEST_TEMPLATE.md`, `CONTRIBUTING.md` (and `docs/CONTRIBUTING.md`), any AI policy file, and `scope.md`'s house rules |
| Issue, Thread highlights | the issue named by URL, read with `gh issue view <N> --comments` |

Substitute the repo's default branch for `main` if it differs.

## Plan fidelity (harness category: silent-drift)

**Where it lives**
- Eval: `## Plan context`. The plan's committed change steps are in
  the "Plan:" paragraph ("Scope, one bounded change: ..."). Its
  boundary is the "Files:" list and the "Not in scope:" line. A
  recorded deviation is a "Deviation note" paragraph inside the plan
  context. What actually changed is every `--- a/` / `+++ b/` file
  header and hunk in `### Diff`. The description's fidelity claims
  ("implements the plan exactly", "no changes beyond it", "tests
  added") and any restated deviation or deferral are in
  `### Description`.
- Live: the steps, Files list, Not-in-scope line, and Deviations
  section of `plan.md`; the file list from
  `git diff --stat main...HEAD`; `pr_draft.md` for the claims.

**What good looks like**
- Every changed file is on the plan's Files list or is a test,
  changelog, or doc file for the fix. Every hunk does a step the plan
  names.
- Every step the plan commits to has a hunk. A step left out is named
  in the Description with a reason ("the cap is in clap's parser, so
  no change to `walk.rs` was needed").
- An honest deviation appears in two places: the plan context records
  what changed and why, and the Description says the same thing. Both
  are needed. A deviation that shows up only in the diff is silent
  drift, however reasonable the change.
- Drift goes in both directions. More than the plan: a dependency
  bump, a refactor of a neighboring function, a second bug fixed
  "while in there", a file the plan put out of scope. Less than the
  plan: a planned test or a planned code site missing with no note.
- The Description promises only what the Diff contains. "Implements
  the plan exactly, no changes beyond it" next to an unrelated hunk
  is silent drift, not a wording problem.

## Test evidence (harness category: not-tested)

**Where it lives**
- Eval: `### Test evidence`, read against the "Test plan:" sentence
  at the end of `## Plan context` (each repro, failure mode, and
  control it names) and the "Repro evidence" paragraph (the failing
  before-result). Repo check commands are named in the Test plan, the
  repo-facts "pull requests" line ("pass the test suite (yarn test)",
  "pre-commit"), and the contribution policy ("cargo fmt, clippy,
  cargo test").
- Live: `test_evidence.md`, read against the Test plan in `plan.md`.
  Path Review names five CI jobs (`lint`, `typecheck`, `test-unit`,
  `test-integration`, `frontend`) and the local commands
  `make check && make test-unit`.

**What good looks like**
- The same command as the repro, run on the branch, with the
  after-output pasted: `$ fd -j 9223372036854775807 .` then the
  argument error and `echo $?` printing `2`, next to the before-result
  (`capacity overflow (exit 101)`).
- Every failure mode and control the Test plan names is shown, or
  named as not run with a reason. If the plan names two repros and the
  evidence shows one with no word about the other, that is not tested.
- Repo checks name the command and show the outcome: "`cargo test`
  passes (614 tests)", or the failing test and why it is unrelated.
- Not evidence: "(none provided)", "tests pass", "works on my
  machine", "the library update looks right", or a run of a different
  behavior from the one the plan targets.

## Diff quality (harness category: unreviewable)

**Where it lives**
- Eval: every hunk in `### Diff`, and the file paths in its headers.
  `### Commits` shows how the work was split (a "gofmt" or "debug"
  commit points at the hunks to inspect).
- Live: `git diff main...HEAD`, and `git diff --stat main...HEAD` for
  committed files that should not be there.

**What good looks like**
- A reviewer sees the fix, its test, and any changelog or doc entry
  asked for, and nothing else.
- Debris tells: added print or log calls not in the plan; blocks
  commented out instead of deleted; new functions or variables never
  used; hunks that only reflow, reorder, re-indent, or merge lines the
  fix does not otherwise change (`a = x` / `b = y` collapsed to
  `a, b = x, y`); renames or restructures the fix does not need; a
  lockfile or dependency change the plan does not name.
- Working notes are never committed: `plan.md`, `pr_draft.md`,
  `test_evidence.md`, or any notes or scratch file appearing as a
  `+++ b/` path fails the diff.

## Standards and comms (harness category: standards-wall)

**Where it lives**
- Eval: the repo-facts "pull requests:" line (template sections,
  checklist items, title convention, "closes #" asks, changelog asks,
  restrictions such as "not accepting new features" or "new linters
  need an approved discussion"). The "contribution policy" line (AI
  policy, CLA, private-API rules). `## Thread highlights` lines from
  OWNER, MEMBER, or COLLABORATOR accounts (CONTRIBUTOR and NONE lines
  are opinions, not direction). The PR side is `### Title`,
  `### Description` (sections, checklist answers, issue link,
  disclosure), and the `### Diff` file list (is the asked-for
  CHANGELOG or test file there?).
- Live: `.github/PULL_REQUEST_TEMPLATE.md`. Path Review's sections are
  Summary, Issue (`Closes #`), Changes, Testing (the checklist,
  including CI green on all five jobs), Screenshots / Demo, and Notes
  for Reviewers. Then `CONTRIBUTING.md` (conventional commits, branch
  `<type>/<issue-number>-<slug>`, complete template), `scope.md`'s
  house rules (fork branch `fix/<issue-number>-<slug>`, template
  always used, disclosure section filled where it applies; course
  work is AI-assisted by design, so in live mode it always applies),
  and the live thread.

**What good looks like**
- Each ask is met with content about this PR. A section with only the
  template's placeholder text, or "N/A" on a section that applies, is
  not met. A checklist item that does not apply says why ("docs n/a,
  no API change").
- An asked-for artifact is in the diff, not only promised: the
  CHANGELOG line, the whatsnew entry, the test file.
- The PR stays inside stated restrictions. A feature PR to a repo
  that is "not accepting new features", or a change to code the
  policy reserves to someone else, is a wall however good the diff is.
- Maintainer direction in the thread is followed, or named and
  answered.
- AI disclosure is checked against the policy only. Every package
  counts as AI-assisted. "All AI usage in any form must be
  disclosed, stating the tool used and the extent" requires a
  sentence such as "I used Claude Code to trace the parser and draft
  the test; I reviewed and ran every change." With no AI policy, no
  disclosure is required in eval mode. In live mode, Path Review's
  house rule makes the disclosure required, in Notes for Reviewers,
  in the author's own words.
- Whether the description's claims match the diff is plan fidelity,
  above, not this family.
