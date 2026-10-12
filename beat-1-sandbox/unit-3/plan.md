# Plan: Issue #54 — Resume parsing fails on leading whitespace

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54

## Diagnosis

My Unit 2 reproduction showed that leading whitespace prevents the parser from detecting resume sections. My report states:

> The issue reproduces on main at f89c06f. With the leading whitespace, detected_sections is empty. Without the indentation, the parser detects Skills and Education.
>
> The issue-specific test tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience also produced 1 xfailed in 0.53s.

In `ingestion/parsers/resume_parser.py`, `_detect_sections()` uses regex patterns that expect a section name right at the start of a line. They do not allow spaces or tabs before it.

`_strip_markdown()` makes the same assumption: it removes Markdown headings with `^#+\s+`, so an indented `## Contact` keeps its `#`. The issue body only names `_detect_sections()`, but five tests carry an `xfail(strict=True)` marker for #54, and two of them (`test_parse_markdown_resume`, `test_strip_markdown_syntax`) only exercise `_strip_markdown()`. Other contributors on the issue thread reported that fixing only `_detect_sections()` leaves those two tests failing.

What is confirmed and what is not:
- Confirmed by my repro: indented input gives an empty `detected_sections`.
- Not yet run by me on a branch: that `_strip_markdown()` has the same line-start problem, and that fixing both functions lets all five tests pass. I'm going on my reading of the code and the thread.

## Scope

**In scope**
- Update `_detect_sections()` to allow leading spaces or tabs before section headings.
- Update `_strip_markdown()` to allow leading spaces or tabs before Markdown `#` headings.
- Remove the `xfail(strict=True)` marker from each of the five #54 tests, but only after that test passes (CONTRIBUTING says the marker should go once the fix makes the test pass).
- Add one small regression test for an indented Markdown heading (see Test plan).

**Out of scope**
- Other parsers, `SECTION_HEADERS`, result ordering, and the other Markdown rules in `_strip_markdown()` (links, bold, italic, code).
- Unrelated cleanup or formatting changes.

## Files to change

| File | Planned change |
|---|---|
| `ingestion/parsers/resume_parser.py` | Allow optional leading spaces/tabs in the section patterns in `_detect_sections()` and in the heading regex in `_strip_markdown()`. |
| `tests/unit/test_resume_parser.py` | Remove the five #54 `xfail` markers after each test passes. Add one regression test for an indented Markdown heading. |

## Fix approach

In `_detect_sections()`, allow optional spaces and tabs after the line-start anchor in the two `^`-anchored patterns:

```python
rf"^[ \t]*{re.escape(section)}\s*$"
rf"^[ \t]*{re.escape(section)}\s*[:|-]"
```

The two `\n`-anchored patterns stay as they are. With `re.MULTILINE`, `^` already matches after every newline, so indented headings should be covered by the first two patterns. I'll confirm that by testing, not assume it.

In `_strip_markdown()`, change the heading regex the same way:

```python
re.sub(r"^[ \t]*#+\s+", "", content, flags=re.MULTILINE)
```

Both changes only add optional horizontal whitespace before the existing match, so unindented input should behave as before.

## Test plan

Only my repro results are verified so far (the single xfailed test and the indented/unindented `detected_sections` outputs). Every count below is **expected**, not confirmed, until I run it on my working branch. My earlier trial in a separate copy of the repo, which changed only `_detect_sections()`, produced three `XPASS(strict)` failures; I haven't tried the `_strip_markdown()` change yet.

Existing coverage of the five tests:

| Test | Targets | Plan |
|---|---|---|
| `test_parse_single_column_resume_text` | `_detect_sections()` | Remove marker once it passes. |
| `test_parse_resume_no_work_experience` | `_detect_sections()` | Remove marker once it passes. |
| `test_detect_sections` | `_detect_sections()` | Remove marker once it passes. |
| `test_parse_markdown_resume` | `_strip_markdown()` | Remove marker once it passes. It only checks that the `#` count goes down, so it is a weak check. |
| `test_strip_markdown_syntax` | `_strip_markdown()` | Remove marker once it passes. It only checks the text doesn't start with `#`. |

Because the two Markdown tests are loose, I'll add one regression test that checks an indented heading directly, for example:

```python
def test_strip_markdown_indented_heading(self, parser):
    stripped = parser._strip_markdown("    ## Contact\n    jane@example.com")
    assert "#" not in stripped
    assert "Contact" in stripped
```

Commands, run on my working branch:

1. Baseline before any change:
   ```bash
   .venv/bin/pytest tests/unit/test_resume_parser.py -q
   ```
   Expected: `5 passed, 5 xfailed`.
2. After the two regex changes, with markers still in place:
   ```bash
   .venv/bin/pytest tests/unit/test_resume_parser.py -q -rxX
   ```
   Expected: all five #54 tests report `XPASS(strict)` (shown as failures), meaning each is fixed. If any still xfails, I'll stop and re-check my diagnosis before removing its marker.
3. After removing the five markers and adding the regression test, rerun the file. Expected: `11 passed`, no xfails.
4. Check indented and unindented input directly. Both should detect Education and Skills. I'll compare sorted results because `_detect_sections()` returns a list built from a set.
5. Run the repository checks:
   ```bash
   make check
   make test-unit
   make test-integration
   ```
   Integration tests may need Docker services. I'll also check the CI results on my fork before considering the change done.

## Risks and unknowns

- The `_detect_sections()` change could match an indented line of body text that looks like a section heading.
- The `_strip_markdown()` heading regex uses `\s+`, which can match across a newline. That was already true before my change, but I should check it doesn't behave differently on indented input.
- I haven't run the `_strip_markdown()` fix myself. Whether it makes both Markdown tests pass is expected from the code and the thread, not confirmed.
- The `XPASS(strict)` results and test counts above are expected until I run them on my branch.

## Deviations

Nothing changed; the plan held. The change I built (commit `13bc8ce` on `fix/54-resume-section-whitespace`, PR #147) touches exactly the two files the plan listed:

- `ingestion/parsers/resume_parser.py`: `[ \t]*` added after `^` in the two `^`-anchored patterns in `_detect_sections()` and in the heading regex in `_strip_markdown()`. The two `\n`-anchored patterns are unchanged, as planned.
- `tests/unit/test_resume_parser.py`: the five `xfail(strict=True)` markers for #54 removed, and one regression test, `test_strip_markdown_indented_heading`, added.

The two things the plan marked as expected-but-unconfirmed are now confirmed by my own runs of `tests/unit/test_resume_parser.py`: `5 passed, 5 xfailed` on `main` (`f89c06f`) and `11 passed` on the branch (`13bc8ce`), so fixing both functions does make all five tests pass.
