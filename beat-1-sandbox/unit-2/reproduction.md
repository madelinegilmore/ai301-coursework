# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

madelinegilmore

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/70#issuecomment-6132083861

Hi, I'm a CS college student working on my first issue and I'd like to work on this. On PathReview 0.1.0 (`main` at `99673c7`), `test_parse_standard_readme` is marked `xfail` because the `sample_readme_text` fixture in `tests/conftest.py` is indented four spaces, so `ReadmeParser` reports `heading_count == 0`. My plan is to post a reproduction report here first, then propose a fix that dedents the fixture and removes the `xfail` marker (H-03).

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-howard/issues/70#issuecomment-6133899643

## Repro report for #70

**Environment:** PathReview 0.1.0, `main` at 99673c7 (my fork, no local changes), macOS 26.6.2 (Apple Silicon), Python 3.12.1. Set up per `docs/SETUP.md`: `cp .env.example .env`, `docker compose up -d`, `make setup`.

**Steps:**

1. Run the test as shipped. It's marked `xfail(strict=True)`, so it only reports as xfailed:

```
$ .venv/bin/pytest tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme -v
tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme XFAIL [100%]
============================== 1 xfailed in 0.13s ==============================
```

2. Run the same test with `--runxfail` so the marker is ignored and the real failure shows (no file edits):

```
$ .venv/bin/pytest tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme --runxfail -v
sample_readme_text = '\n    # Weather App\n    A weather forecasting application built with React and OpenWeatherMap API.\n\n    ## Feature...
>       assert result.metadata["heading_count"] > 0
E       assert 0 > 0

tests/unit/test_readme_parser.py:31: AssertionError
FAILED tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme
============================== 1 failed in 0.14s ==============================
```

3. Control: parse the same fixture as-is and dedented:

```
$ .venv/bin/python -c "
import textwrap; from tests.conftest import sample_readme_text as f; from ingestion.parsers.readme_parser import ReadmeParser
t = f.__wrapped__(); p = ReadmeParser()
print('indented:', p.parse(t).metadata['heading_count']); print('dedented:', p.parse(textwrap.dedent(t)).metadata['heading_count'])"
indented: 0
dedented: 3
```

**Expected:** `heading_count > 0` for `sample_readme_text`, which has three headings (`# Weather App`, `## Features`, `## Tech Stack`).

**Actual:** `heading_count` is 0 because every line of the fixture is indented four spaces. Dedenting the same text gives 3, so the parser handles real headings fine and the fixture is the problem, which matches what the issue says.

**Next:** dedent the fixture in `tests/conftest.py` and remove the `xfail` marker (H-03) from `test_parse_standard_readme`, then run `make check && make test-unit` before opening a PR.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Full run: 15/20 (below the bar; category floor unmet: no match in disclosure)
2. Partial run (`--only` pkg-02, 03, 05, 06, 09, 12, 14, 17, 18, 20 + calibration): 9/10
3. Partial run (`--only` pkg-03, 04, 05, 06, 18): 5/5
4. Full run: 19/20 (bar: 18/20: PASS)

**Package analysis**

**pkg-20** (ghostty, `disclosure` category). Gold label: **reject**. My rubric's first full run graded it **accept**; after I added the `ai-disclosure` check it graded **reject**, matching gold.

The repro itself is strong. My first run passed every proof check, for example `behavior-matches`: "Raw output ^[[?997;2n (single theme) and ^[[?997;1n (conditional pair) matches the issue's 997;2 vs 997;1". The problem is in the repo facts, not the proof. Ghostty's policy says: "All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance". The claim comment says "Hi! I'd like to take this one as a first Ghostty contribution. I reproduced the wrong mode-2031 report on the 1.3.1 release..." and never mentions AI. The gold note says course packages "are treated as AI-assisted work", so that missing disclosure is what holds it.

My rubric accepted it at first because none of my checks read the contribution policy. The only check that looked at the comment at all, `claim-specific`, judged whether the claim was specific to the issue, and it is: "Names 1.3.1 and wrong mode-2031 report with single non-conditional theme". So every check passed and the verdict rule accepted it. A rubric that only checks proof quality can't see a package whose proof is perfect but whose comment breaks the repo's rules.

**Check rationale**

| ai-disclosure | `repo_facts` contribution policy; `claim_comment_markdown` and `repro_report_markdown` | Treat every package as AI-assisted work. If the repo's stated policy requires disclosing AI use, the comment or report must disclose it (what tool or assistance was used). Pass if it discloses, or if the policy does not require disclosure (permissive, responsibility-only, or human-written-comments rules), or if no policy is stated. Fail only when disclosure is required and absent. | required |

This check didn't exist in my first run. That run scored 15/20, and the `disclosure` category was 0/1, so I failed the category floor even before counting the other misses. pkg-20 was accepted because nothing in my rubric read the AI policy.

It's written as a conditional on the policy, not as "the comment must disclose AI use", because most repos in the set don't require disclosure. My evidence guide already said: "AI-use disclosure is checked only against the policy. If the policy requires it and the draft omits it, that's a problem. If `repo_facts` states no requirement, the absence isn't a failure." A blanket rule would have rejected good packages like pkg-05, where conda's policy says "generative AI tools welcome; you are responsible for all contributions", and pkg-03, where ripgrep's rule is about comments being "written by humans in their own words", not about disclosing. That's why the pass condition names "permissive, responsibility-only, or human-written-comments rules" as passes. I made it `required` because a `preferred` check can never change the verdict, and the disclosure category only counts if pkg-20 is rejected.

**Trade-offs**

The `ai-disclosure` check changes one package: pkg-20 moved from accept to reject. It also costs something on every package, because the grader now has to read the contribution policy and decide whether it "requires" disclosure, and that is a judgment call on vague policies. pkg-07 (p5.js) is the case where it could go wrong. Its policy allows "assistive AI use" and the comment discloses ("Per the AI usage policy: I used an AI assistant to help me organize this report"). If the grader read the policy loosely it could reject a package that disclosed. In the confirming full run, pkg-07 stayed accept, and pkg-03 and pkg-05 (policies that don't require disclosure) also stayed accept, so the check didn't spread past pkg-20.

The same round of revisions loosened two other checks: `steps-followable` (input can be described instead of pasted) and `behavior-matches` (an honest cannot-reproduce passes). Loosening can flip a package that agreed before, so I re-ran canaries with `--only`. Across runs 2 and 3: pkg-02 and pkg-17 (wrong-target), pkg-04 and pkg-14 (no-evidence), and pkg-06 and pkg-18 (unfollowable-comms). All six stayed reject.

One case I accept it will miss: pkg-19. Its repro is fine, but the claim comment is "assign-me" boilerplate promising a guaranteed 2-day fix. My `claim-specific` check catches that ("promises a fix 'within 2 days guaranteed', asks to be assigned, and ignores the open fix PR"), but it is `preferred`, so it can't reject. In run 1, pkg-19 was rejected only because the old, too-strict `steps-followable` also failed it. Loosening that check exposed the gap, so the final run is 19/20 with pkg-19 as the one miss. Making `claim-specific` required would catch it but would also reject pkg-09, whose claim only lacks a version number, so I left it `preferred`.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
