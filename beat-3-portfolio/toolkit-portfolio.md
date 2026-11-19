# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

**Student:** Madeline Gilmore

## Featured Tools

This term I made one real contribution: a Retro theme for the login form of Dimsee, an
open-source React auth library ([issue #62](https://github.com/sidd190/Dimsee/issues/62),
[PR #126](https://github.com/sidd190/Dimsee/pull/126)). These four tools did the work at
the points where it could have gone wrong. issue-scout chose the issue. The voice guard
checked every word I posted to the maintainer. The ship-gate held the PR until the repo's
checks and my own pre-PR rubric passed. The PR monitor read the review and drafted my reply.
Two of them, issue-scout and the voice guard, changed a lot through use. The ship-gate and
the PR monitor barely changed, and their entries say why.

**issue-scout**

**What it is, and the judgment hole I wrote:** issue-scout is a Claude Code skill that finds
a first open-source issue in three stages. It runs `gh search issues` queries across GitHub,
ranks the results using only the fields the search already returned, and grades the top five
against a rubric, check by check. Each grade is pass, fail or unclear, the verdict is accept
or reject, and the output is a plain-language read-out plus one JSON grade per issue. The
skill only provides that funnel. The queries, the ranking filters, the fit profile and the
rubric come empty, and I wrote all four. My search strategy has five queries, and each one
traces to a sentence of my fit profile: TypeScript and JavaScript for "I'd like to get better
at frontend development", Swift for iOS, and Python and Go for the languages I already know.
Every query is limited to `--updated "2026-08-01..2026-10-31"`. The last ranking filter reads:
"Select at most one issue per repository, scanning down the ranked list until five distinct
repositories are represented." My rubric has five checks. Three are required:
`maintainer-alive` ("2 commits in the last 90 days"), `scope-feasible`, and `unclaimed` ("no
assignee, no open linked PR, and no 'I'll take this' comment in the last 14 days"). The
verdict rule is: "accept if every required check passes; preferred checks never change the
verdict, they rank accepted issues; unclear counts as fail."

**How it evolved, dated:** each change below is logged in the skill's own `scan-notes.md`
on the day it was made.

- **2026-11-08, the search window.** My first scans used an open-ended 180-day cutoff. With
  100 results per query, the results bunched up around 2026-05-12, so every candidate was
  about six months stale. I changed all five queries to a three-month `--updated` window and
  added a note to move the window forward before every scan.
- **2026-11-08, `responds-to-issues`.** One repo (desledishant10/vex) only looked responsive
  because its maintainer kept answering their own issues. I added this to the pass condition:
  "maintainer replies to their own issues do not count. If the sample has no
  non-maintainer-authored issue, grade unclear."
- **2026-11-08, a scope check added.** fluent/fluent-operator#1854 passed even though its
  thread was an open debate over broad architecture. I added a required `scope-bounded` check.
- **2026-11-12, that scope check replaced.** `scope-bounded` failed any issue with an
  unresolved design question, which rules out most real issues. I replaced it with
  `scope-feasible`, which fails an issue only when there is no single piece of work in it: "a
  codebase-wide checklist, an 'improve X everywhere', or a container issue tracking many
  sub-tasks". Open design questions now set a difficulty note (straightforward, moderate or
  ambitious) instead. The rubric says the note "never changes accept or reject".
- **2026-11-12, grading by URL.** The scan over the new window found nothing I wanted, so I
  picked three issues from firstissue.dev, a curated list, and had the scout grade them
  directly. The first regrade ran headless and couldn't reach GitHub, so it graded nothing
  until I allowed read-only `gh` commands for that run.

**Evidence:** the 2026-11-08 scan rejected two issues that would have hurt me: asim266/macvis#6
failed `maintainer-alive`, and runbox/runbox7#284 failed `unclaimed` because other people
already had linked PRs open. The 2026-11-12 regrade under the new rubric accepted the issue I
went on to ship. This is its grade, cut down from the read-out:

```json
{"item": "https://github.com/sidd190/Dimsee/issues/62",
 "checks": [
  {"name": "maintainer-alive",   "grade": "pass",    "evidence": "5 most recent commits all dated 2026-11-12 (sidd190, mhd-ali-houria)"},
  {"name": "responds-to-issues", "grade": "unclear", "evidence": "6 most recently updated issues (#104-109) all opened by owner sidd190 today with no comments; no non-maintainer issue in sample"},
  {"name": "shipped-recently",   "grade": "pass",    "evidence": "PR #54 by mhd-ali-houria merged 2026-11-12T11:10Z"},
  {"name": "scope-feasible",     "grade": "pass",    "evidence": "One theme: scoped class in frontend/src/components/AuthForm.css + README design-prop row + screenshots"},
  {"name": "unclaimed",          "grade": "pass",    "evidence": "assignees: []; 0 comments; timeline shows only label events, no linked PRs"}],
 "verdict": "accept"}
```

The read-out ranked it first of three, with the difficulty note "straightforward" because the
issue names the one file to change. It also reported something no check measures: "The owner
merged a newcomer's PR (#54) 24 minutes after it was opened, today." The scout actually graded
#59, the Terminal-theme sibling of this issue. I switched to #62 (same labels, file and
acceptance criteria, Retro theme instead), rechecked `unclaimed` on #62 by hand the same day,
and updated the read-out to name it. I claimed #62 and opened PR
[sidd190/Dimsee#126](https://github.com/sidd190/Dimsee/pull/126), which adds the theme
in `AuthForm.css` and a row in the README.

**Voice guard**

**What it is, and the judgment hole I wrote:** the voice guard is a Claude Code hook. A Python
script, `check_voice.py`, runs before any `gh issue comment`, `gh pr create` or
`gh pr comment` goes out. It reads the text about to be posted, checks it against my voice
guide, and stops the command if a rule is broken. I can also run it by hand on a draft file.
Every check, pass or stop, adds one line to `guard-log.md`. The script is the course's. The
voice guide is mine, and it is the only thing the guard judges by. It has three general
rules, four rules for PR titles and descriptions, a "Things I never post" list, and an
Upstream section of rules for claims, questions and pings. Two of the rules that fired on my
real posts, quoted exactly (the typo is mine):

> Rule: No deadlines
> No timeline promisses.

> Rule: AI disclosure in my own words
> I say which tool I used and what it helped with, every time.
> - Wrong: "AI was used."

**How it evolved, dated:**

- **2026-10-12 (commit `030d7d2`), first guide.** For my unit-2 repro-check I wrote three
  rules: no deadlines, "Name the version and the behavior", and "Write more formally than you
  would text a friend, but no bot voice". The guide also had a never-post list ("I'll have a
  PR up this week.", "Tests pass." without naming which tests).
- **2026-10-14 (commit `91f745b`), a second copy grows.** For pr-precheck I added four PR
  rules: title says what changed, only claim what I showed, say what I left out, and AI
  disclosure in my own words. I added them only to pr-precheck's copy. That left three
  `voice-guide.md` files, one per checker skill, already out of step with each other.
- **2026-11-12, one guide and a hook.** Before posting anything on a real repo, I merged the
  three copies into one file. Each skill's `voice-guide.md` is now a link to that file, so
  editing one rule changes it everywhere. I added the Upstream section, for example
  "never claim over someone: If someone already asked to work on it or is assigned, I ask
  them first instead of claiming it", and installed the guard as a hook. To test the wiring
  I ran `gh issue comment --help`, and the hook stopped it at 15:43. That proved the hook
  runs before anything posts.
- **2026-11-15, the link reached past a skill's folder.** My first plan-check run skipped
  its voice check because the linked guide sits outside the plan-check folder and the run
  couldn't read it. For the second run I gave it access to the voice-guard folder, and the
  voice check ran.

**Evidence:** the first six lines of `guard-log.md`, from the claim through PR #126:

```text
- 2026-11-12 15:43 [hook] stop: no body the guard can read (interactive and --help forms are stopped on purpose) | target: gh issue comment --help
- 2026-11-12 18:58 [manual] stop: rule broken: "No timeline promisses." | target: .../ai301-unit6-starter/claim-draft.md
- 2026-11-12 19:16 [hook] pass | target: gh issue comment 62 -R
- 2026-11-15 15:14 [hook] stop: no body the guard can read (interactive and --help forms are stopped on purpose) | target: gh pr create --help
- 2026-11-15 17:50 [hook] stop: browser posting skips the guard | target: gh pr create --web --repo
- 2026-11-15 17:51 [hook] stop: rule broken: "I say which tool I used and what it helped with, every time." | target: gh pr create --draft --repo
```

The 18:58 stop caught a "within a week" line in my claim draft. I didn't keep that first
version. I deleted the date, and the guard passed the claim through the hook 18 minutes later.
This is the claim as posted on issue #62 (2026-11-13 00:16 UTC), with a first step and a
question in place of a date:

> Hi! I'd like to work on the Retro theme for an open-source course assignment. This would
> be my first contribution here. My first step is to get AuthForm running on current main
> and look at how the existing themes handle signin, signup and error states. Then I'll post
> a short plan for the .auth-container.retro styles here. Is it okay if I take it?

The owner replied "Welcome! Feel free to go ahead and raise a PR for this!" and assigned me.
The 17:51 stop came three days later: my PR description had no AI disclosure. Before PR
#126 went up, I added one that names the tool and what it did: "I used Claude Code to help
find the theme code, and build a local preview page."

**Ship-gate (my ship manifest and pr-precheck)**

**What it is, and the judgment hole I wrote:** the ship-gate is a Claude Code hook on
`gh pr create`, and I can also run it by hand as `check_gate.py`. It does two things in
order. First it runs every check in my ship manifest in a fresh login shell from the
clone's root. Then it runs my pr-precheck skill, which grades the branch's diff against my
`plan.md`, my `test_evidence.md` and the PR title and description I've drafted. If either
part fails, the PR doesn't open. Every run adds a dated entry to `gate-log.md`. I wrote both
judgment parts. The **manifest** lists four checks, each traced to Dimsee's CONTRIBUTING.md
and its CI file: `npm run lint`, `npm test -- --ci --runInBand`, `npm run build` and
`npm pack --dry-run --ignore-scripts`. It also leaves one check out on purpose, with a date
and a reason: `npm run format`, "2026-11-15 ... `npx prettier --check .` on unchanged main
(805e9f4) reports 36 files already unformatted, so running it would add unrelated files to
my PR." The **pr-precheck rubric** has seven checks. Six are required, among them
`diff-matches-plan`, `behavior-proven` and `repo-asks-met`, which reads: "List every ask
those lines state, then check each one. ... Fail on the first ask that is not met."

**How it evolved, dated:** this tool barely changed through use, and that was a decision.

- **2026-10-13, the rubric.** I wrote `description-matches-diff` because of a calibration
  package whose description said "Implements the plan on #19727 exactly, with no changes
  beyond it" while its diff also rewrote `printPropertyKey`. Comparing the diff with the plan
  would catch the extra code, but not the false "exactly". So the description's own claims
  became a check of their own.
- **2026-10-14, eval.** Over 20 graded practice PRs, my rubric matched the answer key on
  20/20 in the first run and 19/20 in the second. The one flip was `pkg-11`: its description
  said "One function touched", but the diff also added a helper, and the grader called that
  loose in one run and false in the other. I chose not to loosen the row, because every
  silent-drift package was rejected in both runs. The cost is that it sometimes fails an
  honest PR that summarizes its changes loosely.
- **2026-11-15, the manifest.** I wrote it the day I gated the real PR. I left out `format`
  after running `prettier --check` on unchanged `main`.
- **2026-11-15, after three real stops, no change.** The gate stopped me three times: a
  missing "before" screenshot, `--web`, and a missing AI disclosure. Each time, the gate
  printed: "If a check asks for something this repo doesn't ask for, fix that check in your
  rubric instead." Each stop asked for something the repo or my own rules really ask for, so
  I fixed the PR and left the rubric alone.

**Evidence:** the gate's first manual run on `feat/retro-theme` (2026-11-15 17:37), from
`gate-log.md`:

```text
- verdict: BLOCK (block)
- manifest checks:
  - lint: `npm run lint` -> ok (1s)
  - tests: `npm test -- --ci --runInBand` -> ok (2s)
  - build: `npm run build` -> ok (1s)
  - package contents: `npm pack --dry-run --ignore-scripts` -> ok (1s)
- pr-precheck checks:
  - behavior-proven [pass]: git grep -n -i retro: '(no output, exit 1)' on 805e9f4 vs 35 matches on af382d5; ...
  - repo-asks-met [fail]: CONTRIBUTING step 5 says 'attach before/after screenshots' but the
    Description's Screenshots section has only after images (retro-signin.png, retro-signup.png,
    retro-errors.png, retro-mobile-390.png); before shots exist but are not included.
```

All four repo checks passed, so a gate that only ran checks would have let this PR through
without the screenshot the repo asks for. I left it out because Claude Code had read only
the theme guide and the issue and told me a "before" shot wasn't needed. I added the before
screenshot, and the next run, at 17:38, passed. The hook passed the PR at 17:56, and it
opened as #126 with head `af382d5`.

**PR monitor**

**What it is, and the judgment hole I wrote:** the PR monitor is a script, `monitor.py`,
that reads my open PR's state on GitHub and sorts it into a named state, such as
`feedback-in` or `nothing-new`. It then chooses one move from my playbook and writes that
move as a draft in `drafted-move.md`, with its reasoning in square-bracket notes. It never
posts. Each run adds a dated entry to `monitor-log.md` and writes a status snapshot to
`run-report.md`. The playbook is mine: response rules, a staleness threshold, nudge
etiquette and walk-away criteria. I set the threshold from Dimsee's own record:

> Waiting for a review ...: 4 quiet days. ... The five most recent merged PRs from outside
> contributors (#114, #110, #55, #54, #52) got a first maintainer response in 0.2 to 49 hours
> (median about 14 hours) ... 4 days is about twice the slowest of those.

The first response rule reads: "My reply opens by answering the reviewer's point in the
first sentence: what I changed and in which commit."

**How it evolved, dated:** this tool barely changed, because only one review cycle has
happened since I wrote the playbook.

- **2026-11-16 16:45, the playbook.** I wrote it after the owner's first review of #126, and
  I haven't edited it since.
- **2026-11-16 16:46, first full run.** The monitor read #126 as `feedback-in` and drafted a
  reply covering CodeRabbit's three findings and the owner's four points.
- **2026-11-16 21:02, second run.** It logged `nothing-new` with the same state fingerprint
  (`5a59f3316511`) and drafted nothing, which was correct.

Nothing so far has tested the staleness, nudge or walk-away rules, so I had no reason to
change them. The real change happened downstream: I didn't post the draft. I did the work
first and rewrote the reply myself.

**Evidence:** the same review point (the switch-mode link's contrast) in the monitor's draft
(2026-11-16) and in the reply I posted (2026-11-17):

> **Drafted:** "The switch-mode link's colors are inline styles in `AuthForm.jsx`, so theme
> CSS can't change them, and a theme PR is CSS only. I can open a separate issue for it if
> you'd like."
>
> **Posted:** "**CodeRabbit, switch-mode link:** fixed in 36dde0e without touching
> `AuthForm.jsx`. Its colors are inline there, so the retro theme overrides them with
> `!important` and keeps the light label behind the link. The link text is now 13.4:1 and
> "Sign In"/"Sign Up" is 12.7:1."

The monitor's own note on that draft told me to do the same:

> [The draft is in future tense because nothing is pushed yet. Do the work first, then change
> each "I'll fix" to "Fixed in <sha>" and open with the commit, per your first Response rule.
> Posting it as is would promise work, not report it.]

The posted reply passed my voice guard (`2026-11-17 14:27 [manual] pass | target:
my-reply.md`). In it, each point opens with its commit (`d3e16b1`, `4951b46`, `36dde0e`,
`d4943a9`), as the playbook asks.

## Inventory

- **issue-select:** the unit-1 skill that grew into issue-scout. It graded one issue per
  call, from a URL or a snapshot file. Its last saved eval scored 18/20 (2026-10-06) but
  stayed below the bar because it accepted the one contribution-policy package. I haven't
  used it on its own since issue-scout replaced it in November.
- **repro-check:** grades a claim comment and a repro report before I post them, against
  five checks, four of them required (`env-recorded`, `steps-followable`, `behavior-matches`,
  `ai-disclosure`). On Dimsee it accepted my repro, after catching that I had
  collapsed the spacing in "raw" `git grep` output and written "renders" for a class I had
  only read in the code.
- **plan-check:** grades a plan and its plan comment against six checks, among them
  `cause-grounded` and `decisive-test`. Its eval scored 19/20 (2026-10-13). On Dimsee it
  accepted my plan twice, but its `procedure.md` has no step for a real issue with no posted
  repro comment.
- **pr-precheck:** grades a branch's diff, plan, test evidence and PR description against
  seven checks before a PR opens, six of them required (among them `diff-matches-plan`,
  `behavior-proven` and `repo-asks-met`). Its eval scored 20/20, then 19/20 (2026-10-14). I
  no longer run it on its own: it runs as the second half of the ship-gate (featured above),
  and its rubric hasn't changed since the 2026-11-15 stops.
- **Repo-memory file (`CLAUDE.local.md` in my Dimsee clone, never committed):** CONTRIBUTING
  conventions, the theme's line ranges, the class list to cover, and the build and test
  commands, written 2026-11-15 from one scoped read of `frontend/`. One line is now out of
  date: it still says to mention the switch link in the PR "rather than fixing it", and I
  have since fixed it.
- **Local preview page (`dimsee-preview/`, outside the repo):** renders the real `AuthForm`
  in headless Chrome, so I can switch theme, mode, OAuth and error states without a backend.
  Phone width uses a 390px iframe, because Chrome on macOS won't make a window that narrow.
  It produced every screenshot on PR #126.

## The Arc

**Beat 1**
Date: 2026-10-06
Friction: my repro-check's first full eval scored 15/20, below the 18/20 bar. It accepted
`pkg-20`, a strong repro on ghostty whose policy says "All AI usage in any form must be
disclosed", from a claim comment that never mentioned AI.
Change: I added a required `ai-disclosure` check that fails only when the repo's stated
policy requires disclosure and the comment or report doesn't disclose.
Result: the next full run scored 19/20 and passed the bar, with `pkg-20` rejected to match
the answer key. Later the same check passed my real Dimsee repro, because Dimsee states
no AI policy.

**Beat 2**
Date: 2026-10-14
Friction: my pr-precheck graded the same `pkg-11` accept in one eval run and reject in the
next, with no file changed between the runs. "One function touched" read as loose in one run
and false in the other.
Change: none. I kept `description-matches-diff` as written, because it rejected every
silent-drift package in both runs, and I wrote down the case it will sometimes miss.
Result: both runs cleared the bar (20/20, then 19/20). On 2026-11-15 the check passed my real
PR description on every gate run, because each claim in it had a matching hunk in the diff.

**Beat 3**
Date: 2026-11-08
Friction: my first issue-scout scans returned results bunched around 2026-05-12, about six
months stale, because the strategy used an open-ended 180-day cutoff.
Change: I gave all five queries a three-month `--updated` window and a note to move it
forward before each scan.
Result: the scan over the new window still found nothing I wanted to take, so I found three
issues on firstissue.dev and had the scout grade them by URL instead.

**Beat 4**
Date: 2026-11-12
Friction: my required `scope-bounded` check failed any issue with an open design question,
and I noticed that most real issues have one.
Change: I replaced it with `scope-feasible`, which fails only issues with no single piece of
work in them, and moved open questions into a difficulty note that never changes the verdict.
Result: the regrade accepted all three URL picks and ranked Dimsee first as
"straightforward". I claimed #62, its Retro sibling, that evening, and the owner assigned me.

**Beat 5**
Date: 2026-11-12
Friction: my voice rules lived in three separate `voice-guide.md` files that had drifted
apart, and I was about to post to a stranger's repo for the first time.
Change: I merged them into one guide that all three skills link to, added rules for claims,
questions and pings, and installed the guard as a hook.
Result: at 18:58 the guard stopped my claim draft on "No timeline promisses." for a "within
a week" line. I deleted the date, and the claim passed and posted at 19:16.

**Beat 6**
Date: 2026-11-15
Friction: all four repo checks passed on my branch, but the ship-gate stopped it twice on my
own rubric's `repo-asks-met`. The first stop was for a missing "before" screenshot that
CONTRIBUTING asks for. The second was for a PR description with no AI disclosure. It also
stopped `gh pr create --web`, because the browser skips both hooks.
Change: I fixed the PR, not the rubric. I added the before screenshot and a specific AI
line, and opened the PR with `--title` and `--body-file`.
Result: the hook passed at 17:56 and PR #126 opened. The owner's first review asked for
OAuth button styling and design polish, neither of which the gate checks.

**Beat 7**
Date: 2026-11-15 to 2026-11-17
Friction: my repo-memory file told me the switch-mode link's inline colors "can't" be
restyled from CSS without `!important` and to leave them for the PR description. At the
first round of review, CodeRabbit measured that link at about 2:1 contrast.
Change: while handling CodeRabbit's second review I reread the base CSS, saw the repo already
uses `!important` on its error border, and overrode the link's inline colors from the retro
rule.
Result: commit `36dde0e` raised the link to 13.4:1 (from 3.2:1 with my first workaround),
`AuthForm.jsx` stayed unchanged, and the JSX question I had planned to ask the owner was no
longer needed.

**Beat 8**
Date: 2026-11-16 to 2026-11-17
Friction: the PR monitor's first draft reply was written in future tense ("I'll fix"),
because nothing had been pushed yet. Its own note warned that posting it would promise work,
not report it.
Change: I pushed the redesign and contrast fixes first, then rewrote the reply in
`my-reply.md` so that each point opens with the commit that addressed it.
Result: the reply passed my voice guard and I posted it on 2026-11-17. The review threads are
resolved, no changes are requested, and the PR is waiting for the owner's next look.

## Limitations and What's Next

Each of my tools checks its own stage, but they don't share what they learn. The scout's
read-out noticed things its rubric doesn't measure: the owner's 24-minute merge of a
newcomer's PR, and a repo created the same day it was graded. Those findings stayed in a
read-out instead of becoming checks. My repo-memory file still says the switch link should
be left alone, two days after I fixed it, because nothing tells me when a fact in it has gone
stale. The checkers grade text and diffs, so nothing in the toolkit looks at what the change
renders. Every visual check on PR #126 was me reading screenshots from my preview page, and
CodeRabbit's six accessibility findings (contrast values, `prefers-contrast: more` versus
`high`, reduced motion on `::after`) all got past every tool I own.

Next I would make three changes. First, add a required repo-age-or-adoption row to
issue-scout (for example, "repo older than 90 days or more than 10 stars"), and change
`responds-to-issues` to count how fast outside PRs get merged instead of only reading issue
replies. Second, add a short accessibility checklist to pr-precheck for UI changes: a real
`prefers-contrast` value, reduced motion reaching pseudo-elements, focus and error states
in every override block, and 4.5:1 text. Third, add a no-posted-repro case to plan-check's
`procedure.md`. Before the PR monitor's staleness and nudge rules can earn trust, they need a
quiet stretch to test them, and #126 hasn't had one yet.

**Tool limits.** One line per featured tool, in the order of the entries above.

issue-scout: it can't tell a real project from a repo made that day, because `maintainer-alive` counts commits and never checks repo age or users (masjid-board, created hours before grading, passed), and `responds-to-issues` came back unclear on all three of my picks because every recent issue was the owner's.
voice guard: it only checks text posted through `gh` from my terminal, so a comment typed on github.com, or a PR opened with `--web`, is never read; it stops `--web` but has no way to see what I then type in the browser.
ship-gate: it grades text and diffs, not what the change looks like, so it passed the branch that CodeRabbit flagged hours later for three contrast problems (a 3.95:1 placeholder, retro rules under `prefers-contrast: high`, which browsers never match, and a switch link near 2:1), and it could only take my word on the screenshots.
PR monitor: its draft is only as current as what's pushed when it runs, so on #126 it proposed declining the switch-link fix as outside a theme PR, a fix I made the next day in CSS alone, and its staleness and nudge rules have not run on a real quiet period yet.
