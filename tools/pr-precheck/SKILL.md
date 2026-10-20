---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Evaluate exactly one PR package per run and answer one question: is this ready to submit?
Treat a PR package as the candidate pull request's title, description, commits, diff, and test evidence. Read these artifacts against the plan they claim to implement, including documented deviations, and the issue the plan belongs to. Do not grade from general impressions or answer a different question.

## Inputs and modes

Use one of two modes: live or eval. Grade only one PR package per run.
1. Live mode
Read these inputs:
- `plan.md`, including `## Deviations`, to understand the planned changes.
- The committed branch diff from `git diff main...HEAD`, run from the working copy.
- The draft PR title and description (for example `pr_draft.md`).
- The test evidence: reproduction steps and actual command output (for example `test_evidence.md`).
The filenames above are examples. If the assignment does not fix the actual names, use whichever files hold these inputs.
- The related issue thread to understand the problem and its discussion.
- `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` for the repository's requirements.
Compare the changes and claims against the plan, issue, test evidence, and repository requirements. For a house-chain student, use the supplied house plan and reproduction pack instead of the student's own plan and reproduction evidence.

2. Eval mode
Use only the supplied package bundle and its text. Do not fetch external information or read any file outside the bundle. Run every rubric check and apply the full verdict rule.
If the mode or required inputs are unclear, report the problem instead of guessing.
Treat the package as the complete source of evidence. If something cannot be verified from the package, do not fill the gap with assumptions.


## The scope seam (live mode only)

In live mode, read scope.md before anything else. Check the actual target repository against the repository listed on the `Repo:` line, and follow the rules in that file.
If the `Repo:` line still contains a placeholder or the target repository does not match the allowed repository, refuse to grade and explain why. Do not guess the correct repository.
In eval mode, ignore scope.md completely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` and check the PR title and description against its rules. Report any rule the draft breaks, with evidence.
Voice-guide violations do not change the verdict on their own. They affect the verdict only if the rubric includes a check for them.
In eval mode, ignore `voice-guide.md`. Apply the rubric's general communication checks instead.

## Component reads

Use `rubric.md` to determine the checks, their pass conditions, and how the final verdict is decided. Use `references/evidence-guide.md` to find the evidence needed for each check. Follow `procedure.md` in the order it specifies.
If the procedure does not explain a step, report the gap instead of making up your own process. If `rubric.md` or `procedure.md` has no actual content, refuse to grade and explain which file needs to be completed.

## Verdict and output

Use only two verdicts: accept means the PR is ready to submit, and reject means it should be held. Follow the verdict rule in rubric.md. You may provide a readable per-check summary before the final JSON block, but the response must end with the exact fenced JSON block below. Include the item identifier, every check's name, grade, and evidence, and the final verdict. Each check `name` must match the check name in `rubric.md` exactly. Ensure the JSON is valid and that nothing follows the block.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Use evidence: Every check must include the fact or quote that supports its grade. Require observable before/after evidence for the fix itself. A named suite-pass statement or control result can support the assessment without full command output when the package provides a specific, credible claim. Do not treat a bare, unanchored claim that 'tests pass' as proof.
- Grade the work, not the polish: Compare the actual changes and claims against the plan, issue, evidence, and repository requirements.
- Follow the rubric: Do not change a grade because you personally disagree with a check's result. If a check needs improvement, revise the rubric.
- Follow the procedure: Use its steps as written and report gaps instead of inventing new ones.
- Treat unclear results carefully: Follow the rubric's verdict rule for `unclear`. If the rule does not say what to do, treat unverifiable claims as failures.