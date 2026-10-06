# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/70

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

````
With your new verdict rule, **#70 and #67 are accepted and #68 is rejected**: #68 already has an open PR.

**Repo-level checks (same for all three):**
- **maintainer-alive: pass.** 3 of the last 5 commits to `main` were made on 2026-09-16, 19 days ago, by collaborator Aburke225.
- **responds-to-issues: fail.** In the 5 most recently updated issues (#69, #62, #64, #53, #57), every comment is from a classmate (author association `NONE`). No maintainer has replied.
- **shipped-recently: fail.** The repo has never merged a PR and has no releases.

Both preferred checks fail, but under your new rule that no longer affects the verdict.

**Ranking of the accepted issues:**
1. **#70, README parser test fixture.** Unclaimed: no assignee, no comments, no PRs.
2. **#67, review creation doesn't verify profile ownership.** Unclaimed: no assignee, no comments, no PRs.

This order isn't backed by anything. Your fit profile in `scope.md` is still the placeholder, and the preferred checks come out the same for both issues. On size alone, #70 is smaller: it fixes a test fixture and removes an `xfail` marker, estimated at 2–4 hours. #67 is an authorization fix in `core/services/review_service.py`. Your rubric doesn't check scope, though, so this isn't a graded reason.

**Rejected:**
- **#68, keyword search `ZeroDivisionError`.** It fails **unclaimed** because open PR #73 (alperensumeroglu, 2026-09-15) says "Fixes #68". The house rule only says classmates' claim *comments* don't block an issue. Your rubric still treats an open linked PR as a claim, so I applied it as written. If you want classmates' PRs ignored too, the rubric or house rule has to say so.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/70",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "3 of last 5 main commits on 2026-09-16 (19 days ago) by collaborator Aburke225"},
      {"name": "responds-to-issues", "grade": "fail", "evidence": "Last 5 updated issues (#69,#62,#64,#53,#57): all comments author_association NONE; no maintainer reply"},
      {"name": "shipped-recently", "grade": "fail", "evidence": "No merged PRs in repo history (PRs #73-#79 all open); releases/latest returns Not Found"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; 0 comments; no PR references #70; no cross-references in timeline"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/67",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "3 of last 5 main commits on 2026-09-16 (19 days ago) by collaborator Aburke225"},
      {"name": "responds-to-issues", "grade": "fail", "evidence": "Last 5 updated issues (#69,#62,#64,#53,#57): all comments author_association NONE; no maintainer reply"},
      {"name": "shipped-recently", "grade": "fail", "evidence": "No merged PRs in repo history (PRs #73-#79 all open); releases/latest returns Not Found"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: []; 0 comments; no PR references #67; no cross-references in timeline"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-howard/issues/68",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "3 of last 5 main commits on 2026-09-16 (19 days ago) by collaborator Aburke225"},
      {"name": "responds-to-issues", "grade": "fail", "evidence": "Last 5 updated issues (#69,#62,#64,#53,#57): all comments author_association NONE; no maintainer reply"},
      {"name": "shipped-recently", "grade": "fail", "evidence": "No merged PRs in repo history (PRs #73-#79 all open); releases/latest returns Not Found"},
      {"name": "unclaimed", "grade": "fail", "evidence": "Open PR #73 by alperensumeroglu (2026-09-15) says 'Fixes #68'; cross-referenced in issue timeline"}
    ],
    "verdict": "reject"
  }
]
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
