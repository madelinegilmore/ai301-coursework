# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**Where it lives**
- Eval bundle: the environment line(s) at the top of `repro_report_markdown`. Compare against `issue.body_markdown` (the issue's own environment line) and `repo_facts.raw_markdown` (latest release, and which versions the bug template asks for).
- Live mode: the top of the draft report. To verify, check the repo's Releases sidebar (the tag and its "Latest" badge), the commit hash beside the latest commit on the main page, and the output of the tool's `--version` command.

**What good looks like**
- Names the tool version, the OS, and a build identifier (tag, commit hash, or a release binary of a named version). Any other versions the bug template asks for (git, runtime) are included too.
- The version tested either matches the version the issue targets, or the report says it differs and why ("issue filed on 0.63.1, I tested 0.64.1").
- If the report says "latest" or "current", the number matches the latest release in `repo_facts`.
- "Locally", "latest", or "my machine" with no version is not an environment record.

## Steps

**Where it lives**
- Eval bundle: the steps and code block in `repro_report_markdown`. Compare against the steps in `issue.body_markdown`.
- Live mode: the steps section of the draft report, plus the repo's README and CONTRIBUTING for how to build or run it.

**What good looks like**
- A stranger could run them from a fresh state in order: how the input was created, the exact command or keypresses, and a command that shows the result.
- Nothing depends on unstated state (an existing file, a config, a prior session).
- Steps that are prose-only ("I ran it on a file") are not followable.
- Steps may differ from the issue's, but then the report says how, and the outcome still matches.

## Behavior shown

**Where it lives**
- Eval bundle: the observed or actual part of `repro_report_markdown` (terminal output, command results, described screen state). Compare against the outcome stated in `issue.body_markdown`.
- Live mode: the pasted log or screenshot in the draft. Never judge from the summary sentence alone.

**What good looks like**
- The artifact shows the same outcome the issue reports: same error text, exit code, or visible result. A different failure is an adjacent behavior, not a match (for example, `exit 2` config error where the issue reports a panic with `exit 101`).
- The artifact is the raw output, not a paraphrase of it.
- Differences in setup (OS, empty repo vs. repo with history) don't matter unless they change the outcome.
- A report that states no actual outcome has not shown any behavior.

## Honesty

**Where it lives**
- Eval bundle: the claim sentences in `claim_comment_markdown` and the summary lines in `repro_report_markdown` ("confirmed", "exactly as described", "same behavior here"), set side by side with the artifact in the report.
- Live mode: the same comparison, between the draft's headline claim and the pasted output.

**What good looks like**
- Every claim is backed by something in the artifact. "Reproduced exactly" holds only if the output matches; if the output differs, the report says so.
- A report that says "could not reproduce", or "reproduced only partly", with what was tried is honest and acceptable. It is not a failure.
- Scope is stated truthfully: if the report tested a newer version or a different OS than the issue, it says "not Termux-specific" and doesn't imply it tested Termux.
- A claim that goes beyond the evidence ("everything in the issue is accurate" after testing one step) is a red flag, even when the rest is detailed.

## Comms

**Where it lives**
- Eval bundle: `claim_comment_markdown` read against `issue.body_markdown`, `issue.state`, `thread_highlights` and `comments_total` (who else is working on this), and `repo_facts.raw_markdown` (bug template fields, contribution policy, AI-disclosure rules).
- Live mode: the issue thread (existing comments, linked PRs, assignees), `.github/` issue and PR templates, CONTRIBUTING.md, and AGENTS.md or CLAUDE.md for AI-tool rules.

**What good looks like**
- Specific: the claim names the version and the behavior, so it couldn't be pasted onto another issue.
- Promises the next artifact (a report, then a fix attempt), not a merge or a deadline.
- Acknowledges what's already on the thread. If `thread_highlights` shows someone claimed the issue or pushed a fix, the claim mentions it. If the issue is closed, the claim shouldn't proceed as if it were open.
- Follows the repo's stated process: it includes the fields the bug template asks for and respects contribution limits (for example, a maintainer who reviews outside PRs only selectively).
- AI-use disclosure is checked only against the policy. If the policy requires it and the draft omits it, that's a problem. If `repo_facts` states no requirement, the absence isn't a failure.
- Honest about being new beats boilerplate. "First contribution, flagging that" reads as signal. "Amazing project!!" and "please assign" read as noise.