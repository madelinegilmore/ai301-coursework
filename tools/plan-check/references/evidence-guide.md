# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

<!-- Where the plan states its cause, and where the repro evidence
pins down the behavior that cause must explain. What it means for a
diagnosis to follow from the evidence rather than contradict or
ignore it. -->

**Where it lives**
- Eval bundle: the cause sits in the candidate plan's Diagnosis or
  "Cause" line (sometimes only in the plan comment's "root cause is"
  sentence). The behavior it must explain sits in the Repro evidence
  block: the numbered steps, every "Control" run, and the Actual line.
- Live mode: the cause is in the draft `plan.md` and the draft
  comment; the evidence is the student's posted repro comment on the
  issue (or, on the house issue, the repro pack as quoted in the
  drafts).

**What good looks like**
- The stated cause predicts every repro observation, including the
  controls. Test it: "if this cause were true, would this control have
  come out the way it did?" If any answer is no, the cause is
  contradicted.
- Controls are the strongest evidence in a package. A control that
  shows the blamed component working (the same items parse without
  the flag; the friendly error prints from the instance path in the
  same build), or the failure occurring with the blamed component out
  of the loop (the slowness with no pager at all), rules that cause
  out.
- A cause borrowed from the thread is held to the same test. A
  confident commenter, a linked PR, or polish in the plan does not make
  it grounded.
- A plan that repeats the cause the repro and a maintainer already
  isolated is grounded even if it is short.

## Scope

<!-- Where the plan bounds itself: the in-scope statement, the
not-in-scope line, the files or areas named. What one bounded change
looks like next to a drive-by rewrite. -->

**Where it lives**
- Eval bundle: the candidate plan's Scope / "In / Out" lines, its
  numbered list of changes, and its Files list; plus any "while
  touching", "while in the area", or "also" items. The plan comment
  often restates the scope ("beyond bumping the default, I plan to...").
- Live mode: the same parts of the draft `plan.md` and comment.

**What good looks like**
- Each committed change is needed to make the reproduced behavior
  correct, or is a regression test or doc line for that fix.
- One bounded change can touch two or three files; size is not the
  test, need is. A plan scoped down to part of the problem, with the
  rest named as deferred and a reason given, is bounded.
- A drive-by rewrite adds commitments the repro never asked for:
  dependency migrations, refactors or state-machine rewrites, new
  options or settings fields, UI rework, CI matrices, ports to sibling
  components, retry frameworks. If any of these is a committed step,
  the plan is unbounded even when the core fix inside it is right.

## Executability

<!-- Where the plan says what will actually be done: files or areas,
approach, order of work. What it means for a stranger to be able to
start executing without asking the author anything. -->

**Where it lives**
- Eval bundle: the candidate plan's Files list, Approach / Change
  steps, and any hedge words ("somewhere", "whichever is easier",
  "not sure", "maybe also", "investigate", "profile", "poke around").
- Live mode: the draft `plan.md`.

**What good looks like**
- A stranger knows where to open the code (a file, function, or named
  code site) and what to change there, without asking the author.
- One approach is chosen. Open questions about details (exact
  threshold, per-use vs per-site check pending a benchmark) are fine;
  open questions about which layer or which file to change are not.
- "Profile it, then optimize what's hot" or "dig into the editor code
  this weekend" is an investigation, not a plan.

## Test plan

<!-- Where the plan says how success will be observed, and how that
maps onto the repro evidence's steps and artifacts. What a decisive
test plan names that a vague one does not. -->

**Where it lives**
- Eval bundle: the candidate plan's Test / Test plan section, read
  against the Repro evidence block's steps and Expected line.
- Live mode: the test plan in the draft `plan.md`, read against the
  student's posted repro.

**What good looks like**
- It re-runs the repro (or a regression test built from it) and names
  the result that proves the fix: the exact output line, exit code,
  color flip at step 3, timing, or printed path.
- The observable would differ before and after the fix; extra checks
  (controls unchanged, the full suite still green) are welcome on top.
- Not decisive: "run the full test suite and make sure nothing
  regresses" alone, "undo works", "should feel fast", "nothing else
  feels broken". These name no observable for the fix itself.

## Honesty

<!-- Where claims meet uncertainty: risks, unknowns, and deviations.
How to tell stated unknowns from false confidence, and where an
honest mid-build deviation gets recorded. -->

**Where it lives**
- Eval bundle: the plan's Risk, open-question, and deferral lines, and
  certainty words in the plan and comment ("the root cause is",
  "definitely", "red herring", "confirmed").
- Live mode: the same in the drafts; after the build, the Deviations
  section of `plan.md` is where an honest change of plan is recorded.

**What good looks like**
- Unknowns are named as unknowns ("untested on Windows; deferred",
  "pending the print benchmark", "maintainers may prefer option 1").
- Certainty is backed by a repro step or control. "The version
  difference is a red herring" when the repro shows the version is the
  deciding variable is false confidence.
- A deviation that changes the build is written into `plan.md` with
  what changed and why, not left only in the diff.

## Comms

<!-- Where the words meet the thread and the repo: the plan comment
read against the issue's maintainer signals (thread highlights, or
the live thread) and against the repo-facts block's stated templates,
contributing asks, and contribution policy (including AI-use
disclosure requirements). What thread-aware looks like next to
boilerplate. -->

**Where it lives**
- Eval bundle: the candidate plan comment, read against the Thread
  highlights (each line carries the author's role: OWNER, MEMBER,
  COLLABORATOR, CONTRIBUTOR, NONE) and the Repo facts block's
  "contribution policy" line (AI policy, review limits).
- Live mode: the draft comment, read against the live issue thread
  (comments, linked PRs, test builds, assignees), CONTRIBUTING.md,
  AI_POLICY.md / AGENTS.md, and `.github/` templates.

**What good looks like**
- Maintainer direction is engaged. When an OWNER, MEMBER, or
  COLLABORATOR has isolated the culprit, chosen or ruled out an
  approach, or posted a test build, the comment follows it or names it
  and says why it takes a different route. A docs-only workaround plan
  that never mentions the owner's code-level culprit and test build is
  not thread-aware.
- Open PRs and prior art are acknowledged ("if #2089 lands first I'll
  rebase my tests onto it").
- AI disclosure is checked only against the stated policy. Every
  package is treated as AI-assisted. If the policy says all AI usage
  must be disclosed (in any form, or in comments), the comment must
  name the tool or the assistance. If it asks for disclosure only in
  pull requests, only requires comments in the author's own words, or
  states no AI policy, the absence of a disclosure is not a failure.
