# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**


[Your GitHub username, exactly as it appears on your profile - no @, no
profile URL. Your comment upstream is identified by this name, and it is
the only thing that ties it to you. Several students may plan the same
house issue, so this is what keeps their comments off your score and
yours off theirs.]

madelinegilmore

**Plan comment**

[Link to the comment where you posted your plan on the issue. Use the comment's own
permalink. **Then paste the text of that comment underneath the link** — the pasted text is
what this field is graded on, so copy across what you actually posted.]

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/70#issuecomment-6154128769

> ## Plan
>
> Following up on my repro report above (PathReview 0.1.0, `main` at 99673c7): with `--runxfail`, `test_parse_standard_readme` fails with `assert 0 > 0` on `heading_count`. When I parsed the same fixture after dedenting it, it gave 3 headings. So the parser is working, and the problem is the four-space indent in `sample_readme_text`.
>
> **Change:** in `tests/conftest.py`, wrap the `sample_readme_text` string in `textwrap.dedent`. In `tests/unit/test_readme_parser.py`, remove the `xfail` marker (H-03) from `test_parse_standard_readme`.
>
> **Not changing:** `readme_parser.py`, since an indented `#` line is a code block in Markdown and shouldn't count as a heading. I'm also leaving `sample_resume_text`, which is indented too, because it isn't part of this issue.
>
> **Test:** re-run my repro steps. The test should go from `XFAIL` to `PASSED`, the `--runxfail` run should pass, and the fixture as shipped should parse to 3 headings. Then `make check && make test-unit` should pass.
>
> I went with `textwrap.dedent` because it keeps the fixture readable, but I can write the string flush-left instead if that's preferred. I'll work on this on `fix/70-dedent-readme-fixture` and open a PR when the checks pass.

---

## Your branch

**Branch**

[The name of the branch you built the change on, exactly as it appears in your fork. The
naming shape is a type prefix, then the issue number, then a short description. **The issue
number in the branch name must be the number of the issue you claimed** — a name carrying
any other number does not satisfy this field.]

fix/70-dedent-readme-fixture

**Evidence**

[Your Unit 2 reproduction steps re-run against the built change: the before, then the
after. Paste both, including the commands you ran and their output.]

Same three steps as my posted repro report, run on `main` at 99673c7 (before) and on `fix/70-dedent-readme-fixture` at 95fd3d3 (after). PathReview 0.1.0, macOS 26.6.2, Python 3.12.1.

Before (`main`):

```
$ .venv/bin/pytest tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme -v
tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme XFAIL [100%]
============================== 1 xfailed in 0.20s ==============================

$ .venv/bin/pytest tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme --runxfail -v
tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme FAILED [100%]
>       assert result.metadata["heading_count"] > 0
E       assert 0 > 0
tests/unit/test_readme_parser.py:31: AssertionError
FAILED tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme
============================== 1 failed in 0.14s ===============================

$ .venv/bin/python -c "
import textwrap; from tests.conftest import sample_readme_text as f; from ingestion.parsers.readme_parser import ReadmeParser
t = f.__wrapped__(); p = ReadmeParser()
print('indented:', p.parse(t).metadata['heading_count']); print('dedented:', p.parse(textwrap.dedent(t)).metadata['heading_count'])"
indented: 0
dedented: 3
```

After (`fix/70-dedent-readme-fixture`):

```
$ .venv/bin/pytest tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme -v
tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme PASSED [100%]
============================== 1 passed in 0.13s ===============================

$ .venv/bin/pytest tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme --runxfail -v
tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme PASSED [100%]
============================== 1 passed in 0.12s ===============================

$ .venv/bin/python -c "
import textwrap; from tests.conftest import sample_readme_text as f; from ingestion.parsers.readme_parser import ReadmeParser
t = f.__wrapped__(); p = ReadmeParser()
print('indented:', p.parse(t).metadata['heading_count']); print('dedented:', p.parse(textwrap.dedent(t)).metadata['heading_count'])"
indented: 3
dedented: 3
```

The test goes from XFAIL to PASSED, the `--runxfail` run goes from `assert 0 > 0` to `1 passed`, and the fixture as shipped now parses to 3 headings instead of 0 (the `indented:` line is the fixture as it ships, and it now matches the dedented control). `make test-unit` on the branch: `376 passed, 52 xfailed`.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

1. Full run: 20/20 (all categories full: clear-accept 7/7, scope-creep 4/4, thread-convention 2/2, unbuildable 3/3, wrong-cause 4/4). No disagreements, so there was nothing to re-run with `--only`.
2. Confirming full run, saved with `--save-run eval-run.txt`, same files: 19/20 (clear-accept 6/7; pkg-14 flipped to reject). Bar: 18/20, PASS.

I also ran the four calibration packages once with `--only calib-01,calib-02,calib-03,calib-04 --include-calibration` (not scored): all four agreed with the gold labels, including the calib-03 trap.

**Package analysis**

[Pick one scored package (`pkg-01` through `pkg-20` — the four `calib-` packages are never
scored). Name it by id, say what your rubric decided and what the gold label said, and
explain why your rubric read it that way.]

pkg-14 (zellij-org/zellij#5174, clear-accept). Gold label: accept. My rubric accepted it on the first full run and rejected it on the confirming run, with `failed: executable, honest-unknowns`.

The plan names the code site ("the client attach/reattach path in `zellij-server` (session connection handling) and `zellij-client`'s terminal query issuance") and picks one approach (drain pending OSC query responses before pane input is wired), but then says "exact functions to be pinned in the PR after tracing the query issuance with debug logs." My executable check fails a plan "if a decision the build depends on is left open (which layer, which file ...)". On one run the grader read "functions to be pinned" as a detail inside a named site, which passes; on the other it read it as an open decision, which fails. The gold says the plan is ready as scoped, and I agree: the layer, the files, and the approach are all chosen, and only the exact function name is left to tracing. The check's wording leaves that line between "site" and "function" to the grader, so this package sits on the edge of it.

**Check rationale**

[Quote one check from the `rubric.md` you uploaded to `tools/plan-check/`, exactly as it reads now.
Then say why it reads that way — what you revised to get there, or what you rejected in
favour of it.]

| executable | The plan's files or areas, approach steps, and any "not sure / whichever / somewhere / investigate" language | A stranger could start the change without asking the author anything: the plan names where the change goes (a file, function, or code site) and commits to one approach. Fail if a decision the build depends on is left open (which layer, which file, "upstream or vendored, whichever is easier", "add recover() somewhere"), or if the plan is "profile / investigate / poke around, then fix what turns up". | required |

It is written to separate an open approach from an open detail. The unbuildable packages (pkg-10 "profile ... optimize whatever the profiling turns up", pkg-17 "gocui? tcell? not sure", pkg-18 "upstream or vendored, whichever is easier") all leave the layer or the approach undecided, so the fail condition lists those exact shapes. I rejected a stricter version that would require named functions, because that would fail honest, ready plans like pkg-14 that name the site but leave the exact function to tracing, and I rejected a looser "names any file" version because pkg-18 ("somewhere around linter execution") and pkg-17 point at an area but still defer the real decision.

**Trade-offs**

[Every check gives something up. Any one of these is a complete answer: a package whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

The executable check gives up stability on plans that name a code site but not the exact function. pkg-14 is the case: same rubric, same files, accepted on run 1 and rejected on run 2. I accept that it may miss pkg-14 on some runs, because loosening the check to "a named site is always enough" risks passing the unbuildable packages that also name an area (pkg-18 points at an area, "a recover() safety net somewhere around linter execution", but leaves the site and the upstream-or-vendored choice open). I did not loosen it: the other 19 scored packages agreed on both full runs, and calib-04 (rejected on its test plan, not on executable) still agreed in the calibration run, so nothing else moved between the runs except pkg-14.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
