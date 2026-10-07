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

JairVilleda

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-6031761182

Picking this up: issue #54 reports that `_detect_sections()` fails to detect resume sections when the text has leading whitespace, leaving `detected_sections` empty. I’ll reproduce this from my environment and post a report with the setup, steps, and observed output before attempting a fix.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54#issuecomment-6032349322

## Reproduction report for #54: reproduced

### Environment

- macOS 15.3
- Python 3.13.12
- pytest 9.1.1
- Commit: `f89c06fc3ff292df2a04a39ac51319d32a76b779` on `main`
- Installed the project in `.venv` with `python -m pip install -e ".[dev]"`

### Reproduction

From the repo root, using the `.venv` interpreter:

I first ran the issue-specific test:

```bash
.venv/bin/python -m pytest tests/unit/test_resume_parser.py::TestResumeParser::test_parse_resume_no_work_experience -v
```

```text
1 xfailed in 0.53s
```

The test is marked `xfail(strict=True)` for issue #54, so it is expected to xfail while the issue is still present.

I then ran the reproduction from the issue:

```python
from ingestion.parsers.resume_parser import ResumeParser
r = ResumeParser()
res = r.parse('\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n')
print(res.metadata['detected_sections'])
```

Output:

```text
[]
```

I also ran the same example without the leading indentation:

```python
from ingestion.parsers.resume_parser import ResumeParser
r = ResumeParser()
res = r.parse('\nJohn Smith\njohn@example.com\n\nEducation:\n- B.S. Computer Science\n\nSkills: Python\n')
print(res.metadata['detected_sections'])
```

Output:

```text
['Skills', 'Education']
```

### Result

The issue reproduces on `main` at `f89c06f`. With the leading whitespace, `detected_sections` is empty. Without the indentation, the parser detects `Skills` and `Education`.

I didn't make any code changes or try to fix the issue yet. I just reproduced the reported behavior and checked it against the unindented version.


## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

19/20
20/20

**Package analysis**

**pkg-12 — accept.** The gold label is **accept**, in the clear-accept category. The gold note says: “both shapes reproduced on the current release with outputs shown; version delta stated; next step concrete”. My rubric decided **accept** in the final run. The final `eval-run.txt` records `pkg-12: accept` and shows `pkg-12  accept  accept  yes`.

The per-check results were not saved, so the final run does not record which individual checks passed. Because the verdict rule says that every required check must pass for an accept, the final accept means that none of the five required checks failed or were unclear.

The earlier 19/20 run rejected pkg-12 with the note `failed: steps-rerunnable`; the other four check results were not recorded. My reading of the package is that the reproduction report gives the environment and says the issue's script was run verbatim, and it describes the two `prettier.format` calls and their ranges. However, it does not include the script or input strings themselves. The issue body contains those inputs and ranges, so I read the steps as followable using the information in the package. This is my interpretation of the package, not saved grader reasoning.


**Check rationale**

“A stranger can follow the steps from the stated starting point to the reproduction attempt using only the information provided. The steps use the issue's actual trigger, including relevant commands, inputs, flags, and configuration. A changed trigger fails unless the change is clearly explained and justified. Required setup cannot be omitted, and the steps cannot depend on private or unavailable material.”

I kept this check strict because the reproduction needs to be independently followable, not just convincing to the person who ran it. I specifically included the issue's actual trigger and relevant inputs, flags, configuration, and dependencies so that changing the trigger or leaving out required setup would not count as a valid reproduction. I also kept the requirement against private or unavailable material so another contributor can actually repeat the result.

**Trade-offs**

I considered loosening `steps-rerunnable` after the first full run gave 19/20 because pkg-12 was rejected for that check. I did not change the rubric. The package contains the issue's script inputs and ranges in the issue itself, so I decided that the existing check could reasonably allow a reproduction report to refer to information already provided in the package rather than requiring every input to be copied into the report. The confirming full run then accepted pkg-12 without any rubric changes and reached 20/20. This showed me that changing the check based on one borderline result was not necessary.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
