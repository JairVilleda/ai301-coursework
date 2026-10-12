# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

JairVilleda

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-6118085927

Plan for #54, built from my repro report above.

On `main` at `f89c06f`, the issue's indented example returns `[]` for `detected_sections`. The same text without the indentation detects `Skills` and `Education`.

The cause looks like line-start matching in `ingestion/parsers/resume_parser.py`. The patterns in `_detect_sections()` expect the section name right after `^` or `\n`, so leading spaces stop the match. Other reports on this thread found that `_strip_markdown()` has the same problem with its `^#+\s+` heading regex, which would explain why `test_parse_markdown_resume` and `test_strip_markdown_syntax` also carry #54 markers. I haven't run that second part myself yet, so I'm treating it as likely, not confirmed.

Planned change:
- Allow optional leading spaces or tabs (`[ \t]*`) in the `^`-anchored patterns in `_detect_sections()` and in the heading regex in `_strip_markdown()`.
- Remove the `xfail(strict=True)` marker from each of the five #54 tests, but only after that test passes.
- Add one small regression test for an indented Markdown heading, since the two Markdown tests only check loosely.
- Nothing else changes (other parsers, `SECTION_HEADERS`, result ordering, other Markdown rules).

How I'll test it: run `.venv/bin/pytest tests/unit/test_resume_parser.py -q` before and after the change. With the fix in and the markers still on, I expect the five #54 tests to show `XPASS(strict)`, which means each is fixed. Then I'll remove the markers and expect the file to pass with no xfails. I'll also compare indented and unindented input directly, and run `make check` and `make test-unit`. I haven't implemented or tested the fix yet.

---

## Your branch

**Branch**

fix/54-resume-section-whitespace

**Evidence**

Two kinds of results are below. The **original Unit 2 results** are copied from my reproduction report (issue comment `issuecomment-6032349322`), run on `main` at `f89c06f` before any fix. The **re-runs** are commands I ran later, during a final check of this submission: each on a clean `git archive` export of one commit, using the project's `.venv` Python. They are not from my original Unit 2 environment. The before re-run is `main` at `f89c06f` and the after re-run is my branch `fix/54-resume-section-whitespace` at `13bc8ce`.

**Before the fix**

Original Unit 2 results (`main`, `f89c06f`):

```bash
.venv/bin/python -m pytest tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience -v
```

```text
1 xfailed in 0.53s
```

The issue's example, with and without indentation, printed `[]` and `['Skills', 'Education']`.

Re-run on the `main` export (`f89c06f`):

```bash
.venv/bin/python -m pytest tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience -v
```

```text
tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience XFAIL [100%]
============================== 1 xfailed in 0.15s ==============================
```

```bash
.venv/bin/python -m pytest tests/unit/test_resume_parser.py -q
```

```text
xx.x..xx..                                                               [100%]
5 passed, 5 xfailed in 0.18s
```

```python
from ingestion.parsers.resume_parser import ResumeParser
r = ResumeParser()
res = r.parse('\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n')
print(sorted(res.metadata['detected_sections']))
res = r.parse('\nJohn Smith\njohn@example.com\n\nEducation:\n- B.S. Computer Science\n\nSkills: Python\n')
print(sorted(res.metadata['detected_sections']))
```

```text
[]
['Education', 'Skills']
```

**After the fix**

Re-run on the branch export (`fix/54-resume-section-whitespace`, `13bc8ce`), with the same three commands and the same inputs:

```text
tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience PASSED [100%]
============================== 1 passed in 0.08s ==============================
```

```text
...........                                                              [100%]
11 passed in 0.09s
```

```text
['Education', 'Skills']
['Education', 'Skills']
```

The indented text now finds both sections, the unindented text is unchanged, and the five #54 tests pass with their `xfail` markers removed (5 + 5 + my new regression test = 11). The whole-file run and the sorted output are not in my Unit 2 report; they are extra checks I added.

## Eval iterations

**Run history**

20/20 agreement.

**Package analysis**

`pkg-06` — Scope-creep category.

My rubric rejected this package, and the gold label was also reject. The plan proposes five changes for a bug where saving a preloaded image creates an empty tar file but exits successfully. Surfacing the export error addresses the reproduced problem. Regenerating tarballs, upgrading containerd, adding a cross-runtime abstraction, and expanding the CI matrix go beyond the issue.

The saved evaluation records the final decision, not individual failed checks. My conclusion that this plan fails the Scope check is based on the package text and rubric.

**Check rationale**

The Scope check in `tools/plan-check/rubric.md` says:

> | Scope | The plan's scope, files to change, and exclusions. | The changes are limited to what is needed to fix the bug, without unrelated work. | required |

I chose this check because it helps keep plans focused on fixing the reported problem instead of adding unrelated changes.

**Trade-offs**

**What the rubric documents:** `Risks and unknowns` is marked `preferred`, and preferred checks do not affect the final verdict.

**My interpretation:** A plan can overstate an unverified result and still be accepted if it passes the required checks. This is a limitation of the rubric because uncertainty may be flagged without changing the verdict.

**Re-runs:** I did not rerun any package with `--only`, so I am not claiming that any package result changed.
