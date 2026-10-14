---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question about one PR package: **is this ready to
submit?** A PR package is a candidate pull request (its title,
description, commit list, diff, and test evidence) read against three
things: the accepted plan it claims to implement (with that plan's
repro evidence and any deviation notes), the issue that plan belongs
to, and the repo's own stated asks (PR template, contribution policy,
maintainer direction in the thread).

Grade exactly one package per run. Do not grade the issue, the plan,
or the code's general quality. Do not suggest a different fix, and do
not answer from gut feel. Every grade comes from executing the
components in this directory.

## Inputs and modes

Decide the mode first. If you were given a package file (a path under
`eval/packages/` or a bundle with `# Eval package:` at the top), you
are in eval mode. If you were asked to grade the user's own branch or
draft PR, you are in live mode.

**Live mode** grades the student's own submission before it goes out.
Read these inputs from the student's working copy of the scoped repo:

- Plan: `plan.md`, including its Deviations section. A house-chain
  student reads the house plan and the house repro pack instead; the
  same checks grade the same things there.
- Diff: everything the branch changes relative to the repo's default
  branch. Produce it with `git diff main...HEAD` (three dots) run from
  the working copy, and get the file list with
  `git diff --stat main...HEAD`. Substitute the default branch if it
  is not `main` (`git symbolic-ref refs/remotes/origin/HEAD` names
  it).
- Commits: `git log --oneline main..HEAD`.
- Title and description: `pr_draft.md`.
- Test evidence: `test_evidence.md`.
- Issue-side evidence, gathered from the real repo: the issue and its
  thread (`gh issue view <number> --comments`, using the issue URL the
  student gives), the PR template at
  `.github/PULL_REQUEST_TEMPLATE.md`, and the stated policy in
  `CONTRIBUTING.md` (or `docs/CONTRIBUTING.md`) and any AI policy
  file.

If an input file does not exist, do not invent its contents. Every
check that reads it grades `unclear` and names the missing file. The
working notes (`plan.md`, `pr_draft.md`, `test_evidence.md`) are
inputs only. If any of them shows up in the diff, that is graded as
debris.

**Eval mode** grades one frozen package. The package file is the
whole world. Every fact comes from its text. Fetch nothing, open no
URL, run no `gh` or `git` command against the source repo, and never
open the issue named on the `source:` line. Grade from the `.md`
file; the `.json` twin carries the same content for the harness.
Eval mode always grades the complete package: every check in
`rubric.md`, and the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before reading anything else.

1. Find the `Repo:` line. If it is empty or still carries an unfilled
   placeholder (text in angle or square brackets, or the words
   "replace with"), stop without grading. Print only this, with no
   JSON block: "Scope not set: fill the `Repo:` line in `scope.md`
   with your section's Path Review repo, then re-run." Never guess a
   scope.
2. Confirm the work lives in that repo. The issue URL must point to
   it, and the working copy's `origin` or `upstream` remote
   (`git remote -v`) must be that repo or a fork of it. If either
   points elsewhere, refuse. Print only "Out of scope: this tool
   grades pull requests against `<scoped repo>` only", with no JSON
   block.
3. Treat the scope's house rules as stated asks of the repo. They
   join the PR template and CONTRIBUTING.md in the evidence for
   repo-asks-met: a PR from the fork's `fix/<issue-number>-<slug>`
   branch, one PR per issue, and every template section filled with
   real content, including the disclosure. A classmate's PR on the
   same issue is never a reason to reject.

In eval mode, ignore `scope.md` entirely. Do not read it.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after grading the checks and
before writing the summary. Hold the outgoing PR text, the title and
the description in `pr_draft.md`, against every rule and every
"never post" line in it. In the summary, list each rule the draft
breaks: the rule's name, the line from the draft that breaks it, and
the guide's "Right" example. No rubric check reads the voice guide,
so a broken voice rule never changes the verdict. It is the student's
own standard, reported for them to fix.

In eval mode, ignore `voice-guide.md` entirely. Voice is personal and
carries no gold labels; the communication checks that apply to
everyone live in `rubric.md`.

## Component reads

Read and use the components in this order:

1. `rubric.md` defines the checks (name, evidence, pass condition,
   weight) and the verdict rule. It is the only source of checks and
   of the verdict rule. Do not add, drop, or soften a check at
   runtime.
2. `references/evidence-guide.md` is the map. For each evidence
   family it says where the evidence sits in a package (and, live,
   in the working copy and on GitHub) and what good looks like.
3. `procedure.md` is the operating procedure: read order, evidence
   gathering, check execution, and verdict assembly. Execute it as
   written, step by step. If a step is missing or ambiguous for the
   package in front of you, do the nearest step the procedure does
   give. Then name the gap in one line of the summary ("procedure
   gap: ..."). Never quietly invent a step.

Refusal rule: if `rubric.md` has no filled checks-table row and verdict
rule, or `procedure.md` has no written steps (instruction comments do
not count), stop without grading. Say "pr-precheck cannot grade:
`<file>` has no content. Write the rubric and the procedure first."
Emit no verdict. Inventing checks at runtime produces verdicts that
look like judgment and are noise.

## Verdict and output

The verdict is binary. `accept` means submit: open the PR as it
stands. `reject` means hold: fix what the failing checks name first.
There is no third verdict and no score. Reservations go in check
evidence lines, never in the verdict. Assemble the verdict exactly as
`rubric.md`'s verdict rule and `procedure.md`'s verdict assembly say.

Write the reply in this order:

1. A readable summary: one line per check in rubric order (check
   name, P/F/?, and the deciding quote). Then the verdict, the
   deciding check and its evidence, any preferred-check fixes, any
   procedure gaps, and (live mode only) the voice-guide notes.
2. The fenced JSON block below, last. Nothing follows it: no closing
   sentence, no second block.

In the JSON block, `item` is the bundle id from the package header
(for example `pkg-07`) in eval mode. In live mode, no PR exists yet,
so use the issue URL followed by the branch name. Write `checks` in
rubric order, with every check, preferred ones included. Use the
grades `pass`, `fail`, or `unclear` (P, F, and ? in the summary). Each
`evidence` value is one line quoting or naming the fact from the
package that decided it.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

The JSON must be valid: double quotes, no trailing commas, no
comments inside it. Escape any double quote inside an evidence
quote, or switch to single quotes for the quoted text.

## Grading discipline

- Evidence first. Never grade a check without naming the fact or quote
  from the package that decided it. "Looks fine" is not evidence. If
  the evidence is absent, say what is missing and where you looked.
- Grade the thing, not the polish. Read the diff against the plan, the
  test evidence against the test plan, and the description against
  the diff. A terse, complete PR can be ready. A confident,
  well-formatted one can be hiding drift. Length, headings, and tone
  never move a grade.
- The rubric decides, not the run. If a check passes by its stated
  condition but feels wrong, it still passes. Note the tension in the
  summary; the fix belongs in `rubric.md`.
- The procedure decides how, not the run. Follow `procedure.md` as
  written and report its gaps instead of papering over them.
- Unclear defaults to fail. `rubric.md`'s verdict rule says how
  `unclear` counts. Where any rule is silent, treat an unverifiable
  claim as a failing one: a PR you cannot verify from the package is
  not ready to submit.
- Honest shortfalls are not failures by themselves. A dropped step, an
  unrun test, or a failing check that the PR names with a reason is
  graded by the pass condition that covers it, not held against the
  PR on sight.
