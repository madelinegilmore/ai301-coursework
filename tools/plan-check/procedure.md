# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

<!-- What gets read, in what order, before any check is graded, and
what to note down from each part while reading. A complete procedure
decides the order (issue first? repro evidence first?) and says why
the order matters for the checks that come later. -->

1. Read the repro-evidence block first, before the plan. Write down:
   (a) the failing behavior in one line, (b) every control run as
   "changed X -> result", and (c) what each control rules in or out.
   This comes first so the evidence is fixed in your notes before the
   plan's diagnosis can frame it; a confident plan read first makes
   its cause look obvious.
2. Read the issue (title, body, stated expected behavior). Note
   anything the issue says the reporter already tried.
3. Read the thread highlights. Note every line by an OWNER, MEMBER,
   or COLLABORATOR that isolates a culprit, picks or rules out an
   approach, or posts a test build ("maintainer direction"). Note any
   open or linked PRs. Lines by NONE or CONTRIBUTOR accounts are
   theories, not direction.
4. Read the repo-facts block. Copy the contribution policy line, and
   write down whether it requires AI disclosure, and where (comments,
   PRs only, or all usage).
5. Read the candidate plan, then the candidate plan comment.
6. Live mode only: read `scope.md` first of all (before step 1), and
   take the repro evidence from the student's posted repro comment, or
   the repro pack quoted in the drafts on the house issue.

## Evidence gathering

<!-- For each evidence family your rubric's checks name, the concrete
gathering move: which part of the package (or, live, which page or
thread location per your evidence guide) to pull the fact from, and
what to record. A complete procedure leaves no check whose evidence an
executor would have to hunt for. -->

Use `references/evidence-guide.md` for the location of each family.
For each check, write the gathered fact as a short quote before
grading:

- cause-grounded: quote the plan's cause sentence. Next to it, list
  each control from read-order step 1 and answer "consistent / rules
  it out".
- bounded-scope: list every change the plan commits to (numbered
  steps, files, and "while in the area" items in the plan or comment).
  Mark each "needed for the repro fix", "test/doc for the fix", or
  "extra". Items explicitly named as deferred or not in scope are not
  listed.
- executable: quote the files or code sites named, and quote any hedge
  words ("somewhere", "whichever", "not sure", "investigate",
  "profile", "poke around").
- decisive-test: quote the test plan, and next to it the repro step
  and Expected line it maps to.
- thread-and-policy: list the maintainer-direction notes from read
  step 3 and quote the comment sentence that responds to each (or
  write "not mentioned"). Quote the policy's disclosure requirement
  and the comment's disclosure sentence (or "none").
- honest-unknowns: quote the plan's risks or open questions, and any
  certainty claim ("root cause is", "red herring") with the repro fact
  that does or does not back it.

## Check execution

<!-- How one check runs against gathered evidence: in what order the
checks execute, what an executor does when evidence for a check is
genuinely absent, and when a check may be graded without re-reading
the whole package. A complete procedure makes two executors grade the
same package the same way. -->

1. Run the checks in table order: cause-grounded, bounded-scope,
   executable, decisive-test, thread-and-policy, honest-unknowns.
   Grade every check, even after a required check has failed, so the
   output shows the full picture.
2. Apply only the rubric row's pass condition to the facts gathered
   for that check. Do not re-read the whole package for a check; if
   a fact is missing from your notes, go back only to the location
   the evidence guide names for that family.
3. Grade `pass`, `fail`, or `unclear`:
   - `unclear` only when the package genuinely does not contain the
     evidence (for example, the plan states no test plan and no repro
     steps exist to tie one to). Write which location you checked.
   - A missing part that the check needs (no cause, no files, no test
     plan) is a `fail`, not `unclear`: the plan is what's being graded.
4. One cause per fail: for each `fail`, the evidence line quotes the
   single fact that decided it (the control that rules out the cause,
   the extra item, the hedge word, the non-observable test, the
   unanswered maintainer direction, or the missing disclosure).
5. Do not let polish or length move a grade. A short plan that names
   the site, the change, and an observable test passes; a long plan
   with headings fails if its cause is contradicted or its scope adds
   extra work.

## Verdict assembly

<!-- How the per-check grades become the final accept or reject:
apply your rubric's verdict rule, state how unclear grades enter it,
and say what gets quoted in the output for the deciding check. A
complete procedure produces the same verdict from the same grades,
every time. -->

1. Apply the rubric's verdict rule: if any required check
   (cause-grounded, bounded-scope, executable, decisive-test,
   thread-and-policy) is `fail` or `unclear`, the verdict is `reject`.
   Otherwise it is `accept`.
2. `honest-unknowns` never changes the verdict; if it fails, say so in
   the summary as a fix to make before posting.
3. In the summary, name the deciding check first (the first failing
   required check in table order) and repeat its evidence quote. For
   an accept, say which fact made each required check pass.
4. Live mode: after the verdict, hold the draft comment against
   `voice-guide.md` and list any broken rule with the rule quoted.
   This does not change the verdict.
5. End with the JSON block from SKILL.md, every check included, the
   verdict last.
