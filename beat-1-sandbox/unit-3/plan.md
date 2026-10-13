# Plan: issue #70, README parser test fixture is indented

Issue: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/70
Repro: https://github.com/codepath/pathreview-ai301-fa26-howard/issues/70#issuecomment-6133899643
Branch: `fix/70-dedent-readme-fixture` on my fork

## Evidence this plan uses

From my posted repro report (PathReview 0.1.0, `main` at 99673c7,
macOS 26.6.2, Python 3.12.1):

- Step 2, the test run with `--runxfail` so the marker is ignored:

  ```
  >       assert result.metadata["heading_count"] > 0
  E       assert 0 > 0
  tests/unit/test_readme_parser.py:31: AssertionError
  ```

- Step 3, the control, parsing the same fixture as-is and dedented:

  ```
  indented: 0
  dedented: 3
  ```

The heading regex in `ReadmeParser._extract_heading_hierarchy` is
`^(#{1,6})\s+(.+)$`, anchored at the start of the line, so a line that
begins with four spaces never matches.

## Diagnosis

The `sample_readme_text` fixture in `tests/conftest.py` returns a
triple-quoted string whose lines are all indented four spaces, so
none of them start with `#`. The parser is behaving correctly: the
control shows the same text gives `heading_count == 3` once it is
dedented. The bug is in the fixture, not the parser.

## Scope

In scope:

- Dedent the `sample_readme_text` fixture in `tests/conftest.py`.
- Remove the `@pytest.mark.xfail(strict=True, ...)` marker for issue
  #70 / H-03 from `test_parse_standard_readme` in
  `tests/unit/test_readme_parser.py`.

Not in scope:

- `ingestion/parsers/readme_parser.py`. The control shows the parser
  already handles real headings, so it is not changed. Making it
  accept indented headings would be wrong anyway, because four-space
  indentation is a code block in Markdown.
- `sample_resume_text` in the same file, which is also indented. No
  test fails because of it under this issue, and it may belong to a
  different issue, so I am not touching it.
- Any other lint, type, or test cleanup.

## Files

- `tests/conftest.py`: the `sample_readme_text` fixture
- `tests/unit/test_readme_parser.py`: the xfail marker on
  `test_parse_standard_readme`

## Approach

1. In `tests/conftest.py`, add `import textwrap` and return
   `textwrap.dedent("""...""")` from `sample_readme_text`. This keeps
   the fixture readable at its current indentation and produces the
   same dedented text as my repro's control (step 3), which parsed to
   3 headings.
2. In `tests/unit/test_readme_parser.py`, delete the
   `@pytest.mark.xfail(...)` decorator (the three lines above
   `test_parse_standard_readme`). Leave the test's assertions as they
   are.
3. Run `make check && make test-unit`, then commit as
   `test(ingestion): dedent README fixture so headings parse` with
   `Fixes #70` in the body.

## Test plan

Re-run my repro steps against the change:

1. `.venv/bin/pytest tests/unit/test_readme_parser.py::TestReadmeParser::test_parse_standard_readme -v`
   - Before: `XFAIL`, `1 xfailed`
   - Expected after: `PASSED`, `1 passed` (no `XPASS(strict)` failure,
     because the marker is gone)
2. The same command with `--runxfail`
   - Before: `assert 0 > 0`, `1 failed`
   - Expected after: `1 passed`
3. The control from step 3, parsing the fixture as it now ships:
   - Before: `indented: 0`
   - Expected after: `heading_count` is 3 for the fixture as-is
     (`# Weather App`, `## Features`, `## Tech Stack`)

Then `make check && make test-unit` passes with no new failures, as
CONTRIBUTING.md asks.

## Risks and unknowns

- The test also asserts `result.text == sample_readme_text`. Both sides
  come from the same fixture value, so dedenting does not affect it.
  I will confirm this when step 1 passes.
- `textwrap.dedent` keeps the leading newline from the triple-quoted
  string. The heading regex works line by line, so the empty first
  line should not matter. Step 3 of the test plan checks that.
- `sample_readme_text` has only one user (`grep` finds it only in
  `test_parse_standard_readme`), so no other test should change.
- I don't know if maintainers would rather have the string written
  flush-left than wrapped in `textwrap.dedent`. Either one fixes the
  issue. I chose `dedent` because it is what my control ran, and I will
  switch if a maintainer asks.

## Deviations

One change, in the shape of the code only. Approach step 1 said to
return `textwrap.dedent("""...""")` directly. The built fixture
assigns the string to a variable and returns `textwrap.dedent(text)`
instead.

Why: the direct call failed formatting on commit. The repo's
pre-commit hook pins black 24.1.0, which puts the string on the line
after `dedent(`. The CI lint job runs `pip install black`, which
installs the latest black (26.10.1 in my venv), and that version
wants `dedent("""` on one line. Each version rewrites the other's
form, so no layout of the direct call passes both. Both versions
leave the variable form unchanged.

What did not change: the approach (dedent the fixture with
`textwrap.dedent`), the two files, the scope, and the test results.
After the change, the test passes, the `--runxfail` run passes, the
fixture parses to `heading_count` 3, and `make test-unit` shows 376
passed and 52 xfailed. The posted plan comment still describes the
change accurately, so I did not update the thread.

