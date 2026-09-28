# Unit 1 — Issue Selection

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54 

**Verdict output**

```
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/54",
    "checks": [
      {"name": "Maintainer Activity", "grade": "pass", "evidence": "Most recent default-branch commit Sept 16, 2026 by Aburke225 (co-authored with claude), 11 days before today"},
      {"name": "Repository Activity", "grade": "pass", "evidence": "Repo not archived; commit on Sept 16, 2026 is within 90 days"},
      {"name": "Bounded Scope", "grade": "pass", "evidence": "Body names one function (_detect_sections) and one root cause (regex anchors fail on leading whitespace), with three specific failing tests referenced"},
      {"name": "No Active Contributor", "grade": "pass", "evidence": "No assignee, Development sidebar shows no linked PRs, no comments on the issue"},
      {"name": "Contribution Policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md exists and contains no AI-contribution restriction"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60",
    "checks": [
      {"name": "Maintainer Activity", "grade": "pass", "evidence": "Most recent default-branch commit Sept 16, 2026 by Aburke225"},
      {"name": "Repository Activity", "grade": "pass", "evidence": "Repo not archived; commit within 90 days"},
      {"name": "Bounded Scope", "grade": "pass", "evidence": "Body isolates one bug in FaithfulnessChecker.check() with a repro snippet and one named failing test"},
      {"name": "No Active Contributor", "grade": "fail", "evidence": "PR #74 is open, titled to close #60, opened Sept 21, 2026 by another student with a posted fix and test verification"},
      {"name": "Contribution Policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md exists and contains no AI-contribution restriction"}
    ],
    "verdict": "reject"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "Maintainer Activity", "grade": "pass", "evidence": "Most recent default-branch commit Sept 16, 2026 by Aburke225"},
      {"name": "Repository Activity", "grade": "pass", "evidence": "Body isolates one bug in KeywordSearcher.index(), names the exact file and an xfail test to un-mark, with a 2-4hr estimate"},
      {"name": "No Active Contributor", "grade": "fail", "evidence": "PR #78 is open, claims to fix #68, opened Sept 27, 2026 by another student with a completed fix and reported passing checks"},
      {"name": "Contribution Policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md exists and contains no AI-contribution restriction"}
    ],
    "verdict": "reject"
  }
]
```

---

## Eval iterations

**Run history**

agreement: 20/20 scored items  (bar: 18/20: PASS)

**Issue analysis**

issue-01 — rubric decision: accept; gold label: accept. The rubric result matched the gold label because the issue passed all of the required checks, and the verdict rule says an issue is accepted only when all required checks pass.

**Check rationale**

Bounded Scope | Issue body and comment thread | Pass if the issue describes one specific, actionable task with a reasonably clear expected outcome, and there is no unresolved design/architecture discussion, umbrella/tracking scope, or evidence of repeated abandoned implementation attempts | required

I included this check because a first issue should have one clear task that a new contributor can understand and work on without having to make major design or architecture decisions.

**Trade-offs**

This check may reject an issue that a contributor could technically complete but has unresolved design questions or a history of abandoned implementation attempts. I accepted that trade-off because those issues can make a first contribution less predictable and harder to scope.

---

## Selection rationale

**Selection rationale**

1. Issue #54 fits my interests because it is a Python issue involving a bug in the resume parser. The issue also looks small enough to work on within the available time because it focuses on one function and a specific regex problem

2. The verdict correctly identified that #54 has a clear scope, no active contributor, an active repository, and no AI contribution restriction. I also considered that the issue matches my Python experience and would give me a manageable first contribution without requiring me to learn a large new part of the project.

3. I do not expect claiming the issue itself to be very difficult because there was no assignee or linked pull request when I evaluated it. The main challenge will likely be understanding the existing resume parser and its tests before making the fix.


---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
