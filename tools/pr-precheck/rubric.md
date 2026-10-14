# Rubric: is this pull request ready to submit?

Every check reads the candidate PR against the plan context, the
repo-facts block, and the thread highlights. "The plan" below always
means the plan context as excerpted in the package (live: `plan.md`),
including any deviation note recorded in it. Locations are spelled out
in `references/evidence-guide.md`; the order the checks run in is in
`procedure.md`.

A check with no stated weight is `required`.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diff-matches-plan | Every file and hunk in the candidate PR's Diff, read against the plan's change steps, its Files list, its "Not in scope" line, and any deviation note in the plan context; the Description for the deviation restatement and any deferral note | Two directions, both must hold. (1) Nothing extra: every hunk does a change the plan names, or is a test, changelog, or doc line for that change, or is covered by a deviation note that is recorded in the plan context AND restated in the Description. Fail on any hunk that does work the plan does not name (a dependency bump, a refactor, a second bug, a file on the "Not in scope" line) with no such note. (2) Nothing missing: every change step the plan commits to appears in the diff, or the Description says it was dropped or deferred and why. Fail if a committed step is absent with no note. A recorded deviation that changes the approach passes; a deviation that exists only in the diff fails. | required |
| description-matches-diff | Each factual claim in the candidate PR's Description and Title (what changed, which files, "tests added", "changelog added", "implements the plan exactly", "no other changes", "fixes #N"), each checked against the Diff | Every claim about what the PR changes is visible in the Diff, and the Description does not claim fidelity the Diff contradicts. Fail if the Description claims a change, test, or entry the Diff does not contain, or says "exactly", "only", "no changes beyond the plan" (or similar) while the Diff carries a hunk the plan does not name. Leaving out a minor detail is not a fail; a false claim is. | required |
| behavior-proven | The candidate PR's Test evidence section, read against every before/after the plan's Test plan names (each repro command, each failure mode, each control) and the repro evidence's failing result | (1) The Test evidence shows at least one re-run of the reproduced behavior on the branch with the after-result visible as output, exit code, or a named observable that differs from the before-result recorded in the repro evidence or shown alongside it. (2) Every other before/after the plan's Test plan names is either shown the same way or named in the Test evidence or Description as not run, with the reason. Fail if the evidence is absent, is only "tests pass" / "works now" / "looks right", shows a different behavior from the one the plan targets, or silently leaves out a failure mode or control the plan named. | required |
| repo-checks-run | The Test evidence and Description, read against every check command the plan's Test plan, the repo-facts "pull requests" line, or the contribution policy names (a test suite such as `cargo test`, `yarn test`, `go test`, `make test-unit`; linters or formatters such as pre-commit, clippy, `make lint`; CI) | Each named command appears in the Test evidence or Description with its outcome visible: a pass count, "passed"/"ok" output, or the failing items listed. A failing check passes this check only when the PR states the failure and a reason (for example, "fails on main too, unrelated: <test name>"). Fail if a named command is not mentioned, or is reported only as "tests pass" without naming what was run. If nothing in the plan, repo facts, or policy names a check command, grade `pass` and write "no repo check named". | required |
| diff-reviewable | Every hunk in the Diff and every file path in it; the Commits list for files added | The Diff contains only the fix, its tests, and changelog or doc entries the plan or repo asks for. Fail if it contains any of: an added debug print or log line not in the plan (`print(`, `console.log`, `dbg!`, `fmt.Println`, `println!` used for debugging), a commented-out code block, code added but never called, a formatting-only hunk on lines the fix does not otherwise change, a rename or restructure of code the fix does not need, or a committed working-notes file (`plan.md`, `pr_draft.md`, `test_evidence.md`, or any notes or scratch file). | required |
| repo-asks-met | The repo-facts "pull requests" line and "contribution policy" line, and any OWNER, MEMBER, or COLLABORATOR direction in the Thread highlights, each read against the Title, Description, and Diff | List every ask those lines state, then check each one. Pass when every ask is met: each template section asked for is present with content about this PR (not a placeholder or "N/A" on a section that applies); a "closes/fixes #N" link, title convention, checklist item, CHANGELOG/whatsnew entry, or test file is present when asked for; a checklist item that does not apply is marked n/a with a reason; the PR stays inside any restriction the template or policy states (feature freeze, who may change what, private-API bans); and stated maintainer direction is followed or engaged by name. AI disclosure: treat every package as AI-assisted. When the policy requires disclosing AI use in PRs or in any form, the Description must name the tool and the extent of help; when the policy requires human-written text, the Description must not say it was AI-generated. No AI policy, or a policy that only assigns responsibility, means no disclosure is required. Gates met outside the PR (CLA signing, vouching) fail only when the package shows them unmet. Fail on the first ask that is not met. | required |
| title-names-change | The candidate PR's Title | The Title names the behavior that changes or the thing fixed, specifically enough that it could not sit on a different PR ("Reject --threads values above a sane cap instead of panicking"). Fail on effort or mood titles ("fixed the bug!!", "updates", "WIP"). A title convention the repo asks for is graded in repo-asks-met, not here. | preferred |

## Verdict rule

- Grades are `pass`, `fail`, or `unclear` (shown as P, F, ? in the
  readable summary). `unclear` means the package does not contain the
  evidence needed to decide; the evidence line says what is missing.
- `accept` only if every required check (diff-matches-plan,
  description-matches-diff, behavior-proven, repo-checks-run,
  diff-reviewable, repo-asks-met) is `pass`.
- `reject` if any required check is `fail` or `unclear`. An `unclear`
  on a required check counts as a fail.
- title-names-change is preferred: it never changes the verdict, in
  either direction, whatever its grade. When it fails, the summary
  lists it as a fix to make before opening the PR.
- An honestly disclosed shortfall is not a fail by itself. A step
  dropped with a reason, a planned test not run with a reason, or a
  failing check with its cause stated passes the check that reads it,
  as each pass condition above says.
