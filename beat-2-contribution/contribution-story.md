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

Dimsee's `AuthForm` component ships three visual themes (`modern`, `minimal`, `colorful`), chosen with the `design` prop. Issue #62 asks for a fourth, `retro`, with "a retro 90s computing look". That theme doesn't exist yet, so nothing is broken: a feature is missing.

**Expected Behavior**

`<AuthForm design="retro" />` shows a 90s-computing look. All of its styles are scoped under `.auth-container.retro` in `frontend/src/components/AuthForm.css`, so they can't leak into other themes. It works in signin and signup mode, in error states, and on mobile widths, and the README's `design` prop table lists `retro`.

**Current Behavior**

On `main` at `805e9f4`, nothing in `frontend/` or README.md mentions "retro". `design="retro"` would put the class `retro` on the container, but no CSS targets `.auth-container.retro`, so the form would fall back to the shared base styles. The README's `design` options are `'modern'`, `'minimal'` and `'colorful'`.

**Affected Components**

- `frontend/src/components/AuthForm.css`: the only stylesheet, where each theme is a scoped block and the mobile rules live in `@media` blocks.
- `README.md`: the `design` row of the AuthForm props table (line 179).
- `frontend/src/components/AuthForm.jsx`: reads `design` at line 195. It needs no change, but it decides which markup the theme has to style.

**Toolkit**

- Tool: my repo-memory file (`CLAUDE.local.md` in my clone) and the one scoped orientation run behind it. I ran a read-only Claude Code agent over only `frontend/`, asking where theme styling lives, how `design` picks a theme, which classes a theme must cover, and where the tests are, then checked its line numbers against the source.
- What it produced: a short map, distilled into my memory file. One CSS file to edit, the theme block line ranges, the three `@media` blocks to extend, the full class list for signin, signup, errors and OAuth, and the fact that the only frontend test checks the export.
- Difficulties: it found things the issue doesn't mention. The mode-switch link's colors are inline styles in `AuthForm.jsx` (lines 357–368), which a CSS-only theme can't change. A themed input background also overrides the error background, so error states need their own rules.
- What changed: I added those two points to my plan as things to handle (error styles) and things to leave alone and mention in the PR (the inline link colors), instead of finding them halfway through the build.

---

## Reproduction Process

**Environment Setup**

- OS: macOS 26.6.2
- Node v22.14.0, npm 11.2.0
- Dimsee 0.6.9 (from `package.json`; the repo has no GitHub release published)
- Build: upstream `main` at commit `805e9f4` (2026-11-15, "fix: set sameSite on auth cookies and set each cookie once (#110)")
- Setup: I forked the repo, cloned my fork, and added `sidd190/Dimsee` as `upstream`. A stranger can run `git clone https://github.com/sidd190/Dimsee.git && cd Dimsee && git checkout 805e9f4`. I also ran `HUSKY=0 npm ci`, `npm run lint`, `npm test -- --ci --runInBand` and `npm run build` to confirm the project works before changing anything: lint was clean, 44/44 tests passed, and the build succeeded. None of those are needed to see this issue, and no MongoDB is needed.

Challenges: this issue asks for a new feature, so there is no error to trigger. Reproducing it means showing the Retro theme is still missing on current `main`. My shell's `grep` is wrapped by another tool, which gave noisy output and missed one pattern, so I switched to `git grep` pinned to the commit. That gives the same output on any machine.

**Steps to Reproduce**

1. Clone the repo and check out `805e9f4` (command above).
2. From the clone root, run:
   ```
   git grep -n -i retro 805e9f4 -- frontend README.md
   git grep -nE '^\.auth-container\.[a-z]+ *\{' 805e9f4 -- frontend/src/components/AuthForm.css
   git grep -n -F 'auth-container ${design}' 805e9f4 -- frontend/src/components/AuthForm.jsx
   git grep -n -F 'The visual theme of the form' 805e9f4 -- README.md
   ```
3. Observed result: nothing in `frontend/` or README.md mentions "retro" (no output, exit 1). The only theme blocks are `modern`, `minimal` and `colorful`. `AuthForm.jsx:195` puts `design` straight into the class name, and the README's `design` options don't include `retro`. The issue expects `.auth-container.retro` in `AuthForm.css` and `retro` in the README table, and neither exists.

**Reproduction Evidence**

- **Commit showing reproduction:** none (no changes are needed to show a missing feature; the evidence is pinned to upstream commit `805e9f4`)
- **Screenshots/logs:** output excerpt from the commands above:
  ```
  $ git grep -n -i retro 805e9f4 -- frontend README.md
  (no output, exit 1)

  $ git grep -nE '^\.auth-container\.[a-z]+ *\{' 805e9f4 -- frontend/src/components/AuthForm.css
  805e9f4:frontend/src/components/AuthForm.css:26:.auth-container.modern {
  805e9f4:frontend/src/components/AuthForm.css:161:.auth-container.minimal {
  805e9f4:frontend/src/components/AuthForm.css:267:.auth-container.colorful {

  $ git grep -n -F 'auth-container ${design}' 805e9f4 -- frontend/src/components/AuthForm.jsx
  805e9f4:frontend/src/components/AuthForm.jsx:195:    <div className={`auth-container ${design} ${className}`}>

  $ git grep -n -F 'The visual theme of the form' 805e9f4 -- README.md
  805e9f4:README.md:179:| `design`      | `string`   | `'modern'`                   | The visual theme of the form. Options: `'modern'`, `'minimal'`, `'colorful'`.                             |
  ```
- **My findings:** reproduced. The Retro theme does not exist on `main` at `805e9f4`. Because `AuthForm.jsx` has no list of allowed `design` values, reading line 195 shows that `design="retro"` would add the class `retro` with no CSS behind it, so the form would fall back to the shared base styles. I did not render the component to confirm this; a before screenshot of that fallback will go in my PR. The owner (sidd190) already replied to my claim, "Welcome! Feel free to go ahead and raise a PR for this!", and assigned me.

**Toolkit**

- Tool: repro-check, run as `repro-check: grade my claim comment in claim-draft.md and my repro report in repro-draft.md for issue https://github.com/sidd190/Dimsee/issues/62`, with read-only `gh` access allowed for the run so it could check the issue and repo live.
- What it produced: an accept verdict. All four required checks passed (env-recorded, steps-followable, behavior-matches, ai-disclosure), and it checked my commit, version and line numbers against the live repo. The preferred claim-specific check failed because my posted claim said "current main" instead of naming a version or commit, and the voice pass flagged the same thing under my rule "Name the version and the behavior".
- Difficulties: it caught two honesty problems in my first draft. I had collapsed the spacing in the `git grep` output, so it wasn't really raw output, and I wrote that `design="retro"` "renders" a class when I had only read the code, not rendered it. My rubric's structure doesn't fit a feature request well either: "reproduce" here means "show it's missing", so the report has to say so up front.
- What changed: I pasted the raw output and changed "renders" to "would render (I did not render the component)". The claim is already posted, so I can't fix its missing version, but the repro report pins `805e9f4`. Next time my claim will name the commit or version it was written against.

---

## Solution Approach

**Analysis**

The theme is missing because nobody has written it, not because of a bug. `AuthForm.jsx:195` renders `` <div className={`auth-container ${design} ${className}`}> ``, and `design` has no list of allowed values, so any value becomes a class name. Each theme is just a CSS block scoped to `.auth-container.<name>` in `frontend/src/components/AuthForm.css` (modern at lines 26–152, minimal at 161–258, colorful at 267–360). On top of the base rules that apply to every theme, a theme overrides the form, header, inputs, buttons, OAuth buttons and separator. Mobile rules live in `@media (max-width: 768px)` (line 558) and two `@media (max-width: 480px)` blocks (lines 583 and 740). With no `.auth-container.retro` block, `design="retro"` matches nothing and falls back to the base styles. The README's `design` row (line 179) lists only the three existing themes.

Two details shape the fix. First, error states: the base `.form-input.error` border uses `!important`, but a theme's `.form-input` background is more specific than the base error background, so a theme has to style `.form-input.error` and `.error-message` itself to keep errors readable. Second, the "Already have an account? / Don't have an account?" link (`.switch-mode-link`) gets its colors from inline styles in `AuthForm.jsx` (lines 357–368), which CSS can't override without `!important`.

**Proposed Solution**

Add one CSS block, `.auth-container.retro`, to `AuthForm.css` after the `colorful` block, with every rule scoped to that class. The look is a 90s desktop window:
- a teal backdrop
- a light grey panel with square corners and bevelled 2px borders (light on the top and left, dark on the bottom and right)
- a navy title-bar header with white text
- a plain system font stack
- inset bevelled inputs
- a raised button that looks pressed on `:active`
- a dotted focus outline
- no gradients or rounded corners

Error inputs keep a visible red border and a readable background. Then add retro overrides to the existing mobile `@media` blocks, and add `'retro'` to the `design` row in README.md.

What I won't change:
- **`AuthForm.jsx`**, including the inline `.switch-mode-link` colors. CONTRIBUTING's theme guide says themes need "no JavaScript changes", and the issue points to that guide, so I'll mention the link in the PR instead.
- **The other themes and the base rules.**
- **Tests.** I won't add any: the only frontend test checks the export and mocks the CSS, and CONTRIBUTING asks for a test only "where practical".
- **Prettier.** I won't run it. `AuthForm.css` and README.md already fail `prettier --check` on `main`, so running it would reformat both whole files, and I'll match the existing style by hand.
- **Version, CHANGELOG, and anything outside these two files.**

**Implementation Plan**

1. Update local `main` from upstream and create `feat/retro-theme`.
2. Take a "before" screenshot of `design="retro"` falling back to the base styles, using a local preview page that renders `<AuthProvider><AuthForm design="retro" /></AuthProvider>`. The preview stays out of the repo and out of my commits.
3. In `AuthForm.css`, add the `.auth-container.retro` block after the `colorful` block (after line 360). It covers `.auth-form`, `.form-header`, `.form-title`, `.form-subtitle`, `.input-group`, `.input-wrapper`, `.form-input` (`:focus`, `::placeholder`), `.submit-button` (`:hover`, `:active`, `:disabled`), `.button-content`, `.loading-spinner`, `.oauth-buttons`, `.oauth-button` (`.google`, `.github`), `.oauth-icon` and `.separator`.
4. In the same block, style `.form-input.error`, `.form-input.error:focus` and `.error-message` so errors stay visible on the grey panel.
5. Add retro overrides inside the `@media (max-width: 768px)` block and both `@media (max-width: 480px)` blocks, then check `.auth-form *:focus-visible` and `@media (prefers-contrast: high)`.
6. In README.md line 179, add `'retro'` to the `design` options, matching the row's existing formatting.
7. Check it in the preview: signin, signup, submitting an empty form in each mode (client-side validation shows the error states without a backend), and a width of 480px or less. The observable difference: before, `design="retro"` shows the base dark form; after, it shows the grey bevelled panel with the navy title bar, and error inputs keep a visible red border with readable `.error-message` text. Rerunning my repro command `git grep -n -i retro -- frontend README.md` goes from no output to matches in `AuthForm.css` and README.md. Take "after" screenshots of both modes.
8. Run my ship manifest's checks: `npm run lint`, `npm test -- --ci --runInBand`, `npm run build` and `npm pack --dry-run --ignore-scripts`. Confirm `git diff --stat` shows only `AuthForm.css` and README.md.
9. Commit as `feat: add retro AuthForm theme`, push to my fork, and open a PR using the repo's template. It will include `Closes #62`, type `feat`, the checklist, before and after screenshots, a note about the inline switch-link colors, and an AI disclosure in my own words.

Risks and unknowns:
- The exact look is my interpretation of "a retro 90s computing look". The issue doesn't specify colors, so the maintainer may ask for a different palette in review.
- I haven't built the preview page yet. If `AuthProvider` needs more than an `apiUrl` to render the form without a backend (the OAuth status request is expected to fail and be caught), I'll record what I had to do here.
- I can check desktop and narrow widths in one browser on macOS, not on real mobile devices.

Deviations: none yet.


**Toolkit**

- Tool: plan-check, run from my clone as `plan-check: grade my plan in plan.md and draft comment in plan-comment.md for issue https://github.com/sidd190/Dimsee/issues/62`, with read-only `gh` and `git grep` access for the run. I ran it twice.
- What it produced: accept both times, with all five required checks passing (cause-grounded, bounded-scope, executable, decisive-test, thread-and-policy) and the preferred honest-unknowns check passing too. It checked my line numbers against `main` at `805e9f4` and confirmed the owner's "Feel free to go ahead and raise a PR" was the only direction in the thread.
- Difficulties: the first run found that my `plan.md` had picked up the empty Testing Strategy template from my story, and that the voice-guide check didn't run, because the link points outside the skill folder and the run couldn't read it. The skill's procedure also has no step for a real issue with no posted repro comment, so it graded cause-grounded from the repro quoted in my plan plus its own `git grep` check. It couldn't run `prettier --check` itself, so it flagged my Prettier claim as unverified (I had run that check earlier: both files fail on `main`).
- What changed: before grading I added a Risks and unknowns list and a concrete before/after to step 7, so the test names what changes on screen and in `git grep`. After grading I trimmed the stray template from `plan.md`, changed "can't restyle it" to "can't restyle it without `!important`", fixed a claim that the issue (not just CONTRIBUTING) says "no JavaScript", and changed "will pass lint and test" to "I'll run them before opening it". For the second run I gave it access to my voice-guard folder so the voice check ran. I would add a no-posted-repro case to plan-check's `procedure.md`.
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
