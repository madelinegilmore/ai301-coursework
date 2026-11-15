# Contribution: Theme: Retro

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Madeline Gilmore
**GitHub Username:** madelinegilmore
**Issue:** https://github.com/sidd190/Dimsee/issues/62
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 9: Refined my issue-scout profile and clarified the grading workflow**

I used Claude Code to refine my issue-scout fit profile around my Python and Go experience, my goal of improving at frontend work, and my preference for smaller tasks. The grading workflow initially left the expected location for `scan-output.md` unclear, so I confirmed that it belongs in the issue-scout skill directory and will put the grading read-out there after grading my picks. This clarified how I’ll use the scout output in my issue-selection process.

**Unit 10: Installed the voice guard and wrote a repo-memory file for Dimsee**

I merged my three voice-guide copies into one file, added Upstream rules for claims, questions and pings, and installed the guard as a Claude Code hook; the wiring test was blocked on `gh issue comment --help`, which shows the hook fires before anything posts. The manual check then stopped my first claim draft on my own rule "No timeline promisses." because of a "within a week" line, so I took the date out and the revised claim passed the hook when I posted it on Dimsee #62. For the memory file, I found that Dimsee's CONTRIBUTING.md had gained a CI section since my first read (Node 22 and 24 checks must pass), so I reread it before writing `CLAUDE.local.md`. My one scoped orientation over `frontend/` showed that the mode-switch link's colors are inline styles in `AuthForm.jsx`, which a CSS-only theme can't change, so I noted it to mention in my PR rather than widen my scope.

**Unit 11: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 12: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

My first scan on 2026-11-08 ran my search strategy across GitHub: good first issues in TypeScript, JavaScript, Swift, Python and Go, updated in a three-month window. That scan didn't turn up anything I wanted, so I browsed firstissue.dev and gave my scout three issues to grade directly: Dimsee #59 (a Terminal theme for the login form), Ocelot-Social #6616 (a warning for chat messages over 2000 characters), and masjid-board #9 (a Spanish translation). After I patched my rubric's scope check, I graded all three again. The scout accepted all three and ranked Dimsee first, with the difficulty note "straightforward" because the issue names the file to change (`frontend/src/components/AuthForm.css`) and the work is one bounded change. I'm working on Dimsee #62 instead of #59. It's the same task with a Retro theme instead of Terminal, with the same labels, acceptance criteria and file. The scout graded #59, not #62, so I rechecked by hand that #62 was open, unassigned, and had no comments or linked PRs before I claimed it.

The issue fits me because I have three years of coding experience, mostly in Python and Go, and I want to get better at frontend development while keeping my first contribution small. A theme is pure CSS in one file plus one README row, and the repo's CONTRIBUTING.md calls themes "the easiest high-impact contribution." I hope to learn how to scope CSS so it doesn't leak into other themes, how to make a layout work on mobile widths and in error states, and how a real project's PR process works from claim to review. My honest read of the scout is that it held up on scope but missed things about the repos. It accepted masjid-board even though that repo was created the same day it was graded, because `maintainer-alive` counts commits and never checks how old the repo is or whether anyone uses it. `responds-to-issues` came back unclear on all three issues, because every recent issue in those repos was opened by a maintainer, so it couldn't tell me how fast they answer outsiders. Dimsee's owner also filed about 100 issues in one day, which the rubric can't tell apart from a project people actually use. Next I would add a repo age or adoption check and count how fast outside PRs get merged, which would have shown Dimsee merging a newcomer's PR in 24 minutes.

**Claim comment:** https://github.com/sidd190/Dimsee/issues/62#issuecomment-6839843328

**Toolkit**

- Tool: issue-scout (my search strategy and my rubric). I ran a search scan on 2026-11-08, then used `issue-scout: grade <URL> <URL> <URL>` on three issues I found on firstissue.dev, and graded them again after the scope patch.
- What it produced: accept verdicts for all three issues, each with a check-by-check JSON grade. Dimsee ranked first as the best fit, with the difficulty note "straightforward". `maintainer-alive`, `shipped-recently`, `scope-feasible` and `unclaimed` passed, and `responds-to-issues` came back unclear.
- Difficulties: my old `scope-bounded` check rejected any issue with an open design question, which would reject most real issues. The rubric has no check for repo age or usage, so a repo created that day passed. `responds-to-issues` couldn't be graded when every recent issue was opened by the owner. My first regrade, run headless, couldn't read GitHub at all and graded nothing until I allowed read-only `gh` commands for that run. The scout graded #59, so I checked #62 by hand.
- What changed: in step 3 I replaced `scope-bounded` with the `scope-feasible` check, which fails only issues that aren't one piece of work (tracker issues, codebase-wide checklists), and added a difficulty note (straightforward, moderate or ambitious) that never changes the verdict. I logged the change in `scan-notes.md`. I would still add a repo age or adoption check and count how fast outside PRs get merged.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
