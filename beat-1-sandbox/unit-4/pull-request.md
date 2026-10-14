# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

[Link to the pull request you opened. It must be the pull request's own page on the Path
Review repo, not your fork's branch page.]

https://github.com/codepath/pathreview-ai301-fa26-howard/pull/81

**Branch**

[The name of the branch the pull request comes from, exactly as it appears in your fork.
The naming shape is a type prefix, then the issue number, then a short description. **The
issue number in the branch name must be the number of the issue the pull request fixes** —
a name carrying any other number does not satisfy this field.]

`fix/70-dedent-readme-fixture`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1. `agreement: 20/20 scored items  (bar: 18/20: PASS)`
2. `agreement: 19/20 scored items  (bar: 18/20: PASS)` (the saved run in `eval-run.txt`)

I did not change any of my tool's files between the two runs. The second run was only to save the file with `--save-run`, and it graded `pkg-11` differently.

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

`pkg-11` (clear-accept). Gold label: accept. My first run graded it accept. My saved run graded it reject, with the note `failed: description-matches-diff`.

The PR's description says "One function touched, tests added for the escaped, unescaped, and double-backslash cases." The diff changes `parse_gitignore_line` and also adds a new helper, `trim_unescaped_trailing_spaces`. The new test checks the escaped and double-backslash cases, but there is no separate unescaped-only case. My check fails "a false claim" but says "Leaving out a minor detail is not a fail", and it does not say which side a loose count is on. In the first run the grader wrote: "'One function touched' is loose (a helper was added) but not a false claim." In the saved run it read the same sentence as false. Every change the description names is really in the diff, so I think the gold label is right and my wording left room for both readings.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/pr-precheck/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

| description-matches-diff | Each factual claim in the candidate PR's Description and Title (what changed, which files, "tests added", "changelog added", "implements the plan exactly", "no other changes", "fixes #N"), each checked against the Diff | Every claim about what the PR changes is visible in the Diff, and the Description does not claim fidelity the Diff contradicts. Fail if the Description claims a change, test, or entry the Diff does not contain, or says "exactly", "only", "no changes beyond the plan" (or similar) while the Diff carries a hunk the plan does not name. Leaving out a minor detail is not a fail; a false claim is. | required |

This check exists because of calibration package `calib-03`. Its description says "Implements the plan on #19727 exactly, with no changes beyond it," but the diff also rewrites `printPropertyKey` in `property.js`, which the plan never mentions. A check that only compared the diff to the plan would catch the extra hunk, but not that the description promised there wasn't one. I made the description's own claims a separate check, so a PR that hides drift behind "exactly" fails even if the reviewer only reads the description. I put it in the silent-drift family, not comms, because a description that claims more than the diff is drift, not a writing problem.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

This check gives up some stability on loosely worded but honest descriptions. `pkg-11` shows it: the same files graded it accept on run 1 and reject on run 2, because "One function touched" can be read as loose or as false.

I could loosen the row so that only a claim about a change, file, test, or entry that is not in the diff at all fails, and a loose count of a change that is in the diff passes. That loosens a check, so the canary rule would apply: re-run `--only pkg-11` plus one silent-drift package that already agreed (`pkg-03` or `pkg-09`), because those are the packages this check guards. Then I would need a new full run, since a rubric change means `eval-run.txt` no longer matches my files. I chose not to change it. Both runs cleared the bar, and in both runs every silent-drift package (`pkg-03`, `pkg-06`, `pkg-09`, `pkg-17`) was rejected, with `description-matches-diff` failing on `pkg-03`, `pkg-06`, `pkg-09`, and `pkg-17` in run 1. The case I accept it will sometimes miss is an honest PR whose description summarizes its changes loosely.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
