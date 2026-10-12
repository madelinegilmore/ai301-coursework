# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | `repro_report_markdown` (environment line); cross-check `repo_facts.latest release` | Names the tool version, OS, and a build identifier (tag, commit hash, or a release binary of a named version). Fail if any is missing or vague ("locally", "latest"), or if the report claims "current/latest" and the version doesn't match `repo_facts`. | required |
| steps-followable | `repro_report_markdown` (steps and code block), read against `issue.body_markdown` | A stranger could re-run the trigger from a fresh state: the command or keypresses that trigger the behavior are given exactly, and the input is either created by a shown command, shown verbatim, or pinned to content they can get ("the exact 12 lines from the issue", or a minimal input described by the property that triggers the bug, such as "a valid `dependencies:` list plus an unrecognized `category:` section", so any file with that property reproduces it; the contents need not be pasted verbatim). Fail if the trigger command is missing or vague ("ran it on a file"), or if any step depends on state a stranger can't get (a private repo, an unshared config, an unnamed driver or setup the issue depends on). Incidental state that does not change the outcome (packages already installed, an existing directory) does not fail this check. | required |
| behavior-matches | `repro_report_markdown` (actual/observed) vs `issue.body_markdown`; the report's summary lines and `claim_comment_markdown` | Either (a) the raw observed outcome (error text, exit code, or visible result) matches the outcome the issue reports, and setup differences alone don't fail this; or (b) the report honestly says it could not reproduce (or reproduced only partly), shows the artifact of the attempt, and names what differed. Fail if the report or claim says it reproduced the issue but its own artifact shows a different outcome, or if no actual outcome is shown. | required |
| ai-disclosure | `repo_facts` contribution policy; `claim_comment_markdown` and `repro_report_markdown` | Treat every package as AI-assisted work. If the repo's stated policy requires disclosing AI use, the comment or report must disclose it (what tool or assistance was used). Pass if it discloses, or if the policy does not require disclosure (permissive, responsibility-only, or human-written-comments rules), or if no policy is stated. Fail only when disclosure is required and absent. | required |
| claim-specific | `claim_comment_markdown`; `thread_highlights`; `issue.state` | Names the version and the behavior, and promises a next artifact (report, plan), not a timeline or a merge. Fail if the claim could be pasted on any other issue, or if `thread_highlights` shows someone already pushed a fix and the claim doesn't acknowledge it. | preferred |



## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

- reject if any required check fails
- accept if all required checks pass; if a preferred check fails, accept with a note to fix it before posting
