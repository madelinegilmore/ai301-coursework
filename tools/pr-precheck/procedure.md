# Procedure: how this tool grades a PR package

Follow these stages in order. Write notes as you go: every grade later
quotes a note, and every note quotes the package.

## Read order

Read the plan before the PR, and the diff before the description.
The diff has to be measured against the plan, so the plan's limits
must be written down before the diff is read. The description is
read last so that its confident wording cannot frame what the diff
shows.

0. Live mode only: read `scope.md` first, then do the scope gate in
   SKILL.md before anything below. In eval mode, skip this step.
1. `## Plan context`. Write down:
   (a) the failing behavior from the "Repro evidence" paragraph, with
       its before-result (error text, exit code, or output);
   (b) the plan's committed change steps, numbered;
   (c) the Files list and the "Not in scope" line;
   (d) every before/after the "Test plan" names, numbered (each
       repro, each failure mode, each control, each suite command);
   (e) any deviation note, quoted.
2. `## Repo facts`. Copy the "pull requests" line and the
   "contribution policy" line. Turn them into a numbered list of asks
   (each template section, each checklist item, title convention,
   issue link, changelog, tests, restrictions, AI policy). Note
   whether the AI policy requires disclosure, requires human-written
   text, or says nothing.
3. `## Issue` and `## Thread highlights`. Note each OWNER, MEMBER, or
   COLLABORATOR line that gives direction (picks or rules out an
   approach, restates a policy, asks for a specific test). Ignore
   CONTRIBUTOR and NONE lines as direction.
4. `### Diff` and `### Commits`. Build the hunk ledger: one row per
   file, then per hunk, with a few words on what it does.
5. `### Test evidence`. Note each command run and the result shown.
6. `### Description`, then `### Title`. List each factual claim
   (changed X, added test, added changelog, "exactly", "no other
   changes", closes #N), each template section present, and the
   disclosure sentence if any.

In live mode the same parts come from the live sources in
`references/evidence-guide.md`. Read them in the same order:
`plan.md`, the repo's template, CONTRIBUTING.md and the thread,
`git diff main...HEAD`, `test_evidence.md`, then `pr_draft.md`.

## Evidence gathering

Gather one fact set per check before grading any of them.
`references/evidence-guide.md` says where each part lives.

- diff-matches-plan: next to each row of the hunk ledger, write one
  tag: `step N` (a plan step from note 1b), `test/changelog/doc`,
  `deviation` (only if the note 1e covers it AND the Description
  restates it), or `extra`. Then, for each plan step in 1b, write the
  hunk that does it or `missing`. For each `missing` step, quote the
  Description sentence that drops or defers it, or write `no note`.
- description-matches-diff: next to each claim from read step 6,
  write the hunk that shows it, or `not in diff`. Mark any
  "exactly / only / nothing beyond" claim `contradicted` if any hunk
  is tagged `extra`.
- behavior-proven: next to each before/after from note 1d (except the
  suite commands), quote the Test evidence lines that show it, or
  write the Test evidence or Description sentence that says it was
  not run and why, or write `absent`. Mark which item re-runs the
  failing behavior from 1a.
- repo-checks-run: list every check command named in note 1d, the
  repo-facts line, or the contribution policy. Next to each, quote
  its outcome from the Test evidence or Description, or write
  `not mentioned`.
- diff-reviewable: go through the hunk ledger and mark any hunk that
  is a debug print, commented-out code, unused code, formatting-only,
  an unneeded rename or restructure, or a working-notes file. Quote
  the `+` or `-` lines.
- repo-asks-met: next to each ask from read step 2 and each direction
  note from read step 3, quote the Title, Description, or Diff line
  that meets it, or write `unmet`.
- title-names-change: quote the Title.

## Check execution

1. Run the checks in table order: diff-matches-plan,
   description-matches-diff, behavior-proven, repo-checks-run,
   diff-reviewable, repo-asks-met, title-names-change. Grade every
   check, even after a required check fails, so the output shows the
   whole picture.
2. Apply only that row's pass condition to that check's gathered
   facts. Do not re-read the whole package to grade a check. If a fact
   is missing from the notes, go back only to the location the
   evidence guide names for that family.
3. Grade `pass`, `fail`, or `unclear`:
   - `fail` when the gathered facts meet a fail clause. A missing part
     the check grades counts here: test evidence that says "(none
     provided)" fails behavior-proven, because the PR is what is being
     graded.
   - `unclear` only when the package lacks the input the check reads
     (for example, the plan context gives no test plan and no repro
     evidence, or in live mode `test_evidence.md` does not exist). The
     evidence line names the location checked and what was missing.
   - `pass` otherwise.
4. Write one evidence line per check: the single quote or fact that
   decided it. For a fail, quote the extra hunk, the false claim, the
   absent failure mode, the unmentioned command, the debris line, or
   the unmet ask. For a pass, quote the strongest supporting line.
   Every evidence line quotes the package (or, live, the file).
5. One hunk can fail more than one check. An unrelated refactor can
   fail diff-matches-plan, description-matches-diff, and
   diff-reviewable, and each check reports it.
6. Polish and length never move a grade. A terse PR whose diff, proof,
   and asks hold passes. A long, well-formatted one fails on a single
   extra hunk or a single missing failure mode.

## Verdict assembly

1. Apply the rubric's verdict rule. If any required check is `fail`
   or `unclear`, the verdict is `reject`. If every required check is
   `pass`, the verdict is `accept`. title-names-change never changes
   the verdict.
2. The deciding check is the first required check, in table order,
   whose grade is `fail` or `unclear`. Name it first in the summary
   and repeat its evidence line. For an accept, name the fact that
   passed each required check.
3. If title-names-change failed, list it after the verdict as a fix
   to make before opening the PR.
4. Live mode only: hold the Title and Description against
   `voice-guide.md` and list each broken rule with the rule's name
   and the offending line. This never changes the verdict.
5. Report any step this procedure did not cover as a procedure gap,
   in one line in the summary.
6. End with the JSON block from SKILL.md: every check, in table
   order, with the summary's grades; the verdict last. Nothing
   follows the block.
