# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| cause-grounded | The plan's stated cause (its diagnosis or "Cause" line, or the cause the comment asserts) read against every step and control run in the repro-evidence block, especially the controls and the Actual line | The cause is consistent with every observation in the repro evidence: it explains the failing run AND every control (a control that changes one variable and makes the bug go away, or that shows the blamed component working, must fit the stated cause). Fail if any repro step or control shows the blamed component working, shows the failure happening without it, or shows the deciding variable is something else, even when the thread, the issue author, or a confident write-up proposed that cause. Fail if the plan states no cause at all. Not knowing the exact line is fine; blaming the wrong component is not. | required |
| bounded-scope | The plan's list of changes, files, and in-scope / not-in-scope lines, read against the behavior the repro evidence shows | Every change the plan commits to is needed to fix the reproduced behavior, or is a regression test or a doc line for that fix. Fail if the plan also commits to work the repro does not require: a migration or dependency swap, a refactor or rewrite of surrounding code, a new option or setting, UI changes, a CI or build-matrix change, a port to sibling components, or fixing a different bug "while in the area", even if the core fix inside it is correct and even if it is offered as a PR series. Work named as deferred or not in scope does not count against the plan; deferring part of the problem with a stated reason passes. | required |
| executable | The plan's files or areas, approach steps, and any "not sure / whichever / somewhere / investigate" language | A stranger could start the change without asking the author anything: the plan names where the change goes (a file, function, or code site) and commits to one approach. Fail if a decision the build depends on is left open (which layer, which file, "upstream or vendored, whichever is easier", "add recover() somewhere"), or if the plan is "profile / investigate / poke around, then fix what turns up". | required |
| decisive-test | The plan's test plan read against the repro evidence's steps and Expected line | The test names an observable outcome that would be different before and after the fix, tied to the reproduced behavior: re-run the repro steps (or a test built from them) and see a specific result (exact output, exit code, color, timing, file present). Fail if the only test is "run the full suite / nothing regresses", a feeling ("should feel fast", "nothing else feels broken"), or "it works" with no observable named. | required |
| thread-and-policy | The plan comment read against (a) the thread highlights from OWNER, MEMBER, COLLABORATOR, or maintainer accounts and (b) the repo-facts contribution policy, including any AI policy | (a) If a maintainer in the thread gave explicit direction (isolated the culprit, chose or ruled out an approach, posted a test build, asked for a specific kind of fix), the comment either follows that direction or engages it by name and explains the different route. Fail if the comment proposes a plan that sidesteps that direction without mentioning it. Non-maintainer theories in the thread do not count as direction. (b) Treat every package as AI-assisted work. Fail if the stated policy requires disclosing AI use in comments or in any form and the comment does not disclose the tool or assistance. Pass on disclosure if the policy only asks for disclosure in pull requests, only requires human-written comments, only assigns responsibility, or states no AI policy. | required |
| honest-unknowns | The plan's risks, open questions, or deferrals, and any certainty language in the plan and comment ("definitely", "the root cause is", "red herring") | Real unknowns (an untested platform, an approach the maintainers might not want, a side effect) are stated as unknowns, not dressed as certainty. Fail if the plan or comment claims certainty the repro evidence does not support. | preferred |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

- reject if any required check is `fail` or `unclear`
- accept if every required check is `pass`
- `honest-unknowns` is preferred: it never changes the verdict; when
  it fails, report it in the summary as something to fix before
  posting
