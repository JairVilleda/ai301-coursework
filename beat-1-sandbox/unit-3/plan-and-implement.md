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

**Before the fix**

I tested the original `main` branch at commit `f89c06f`.

Command:

```bash
.venv/bin/pytest tests/unit/test_resume_parser.py -q
```

Result: 5 passed, 5 xfailed.

The indented input produced `[]`, while the unindented input produced `['Education', 'Skills']`.

**After the fix**

I tested the same test file on `fix/54-resume-section-whitespace`.

Command:

```bash
.venv/bin/pytest tests/unit/test_resume_parser.py -q
```

Result: 11 passed.

Both indented and unindented input produced `['Education', 'Skills']`.

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

The fix recognizes headings with leading spaces or tabs, supporting more resume formats. However, an indented line of regular text that looks like a heading could also be detected as one. The change is small and leaves the other section-detection patterns unchanged.