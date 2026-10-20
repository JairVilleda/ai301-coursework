# Procedure: how this tool grades a PR package

## Read order

1. In live mode, read scope.md first and confirm the target repository is allowed. This is a gate, not a rubric check: if the Repo line is a placeholder or the repository is not allowed, refuse to grade and stop (see SKILL.md). In eval mode, use only the files in the selected package.
2. Read the plan, including its scope, test plan, and documented deviations. List the files and changes it allows.
3. Read the issue thread (in eval mode, the package's issue and thread sections).
4. Read the diff and note which files changed and what each change does.
5. Read the test evidence and compare the commands and actual output with the plan's test plan.
6. Read the PR description and compare its claims with the diff and test evidence.
7. Find the standards to check against. In live mode, read the repository's PR template and contribution guidelines. In eval mode, read the package's Repo facts section.

Read the plan before the diff so you can judge the changes against the intended scope, not just what the code happens to do.

## Evidence gathering

- Silent drift: Compare every changed file and relevant hunk with the plan's scope and documented deviations. Check each claim in the description against the diff.
- Not tested: Compare the test evidence with the plan's test plan. Record the commands, their actual output, and any missing or unsuccessful checks. A claim without command output is not proof that a test passed.
- Unreviewable: Identify unrelated changes, unrelated commits, or unnecessary code (leftover debug or dead code) that makes the intended fix harder to review, where the available evidence shows them.
- Standards wall: Compare the PR title and description with the standards from read-order step 7: in live mode, the repository's PR template, contribution guidelines, disclosure requirements, and the house rules in scope.md; in eval mode, only the package's Repo facts section. Ignore scope.md in eval mode.
- Record the specific evidence for each check. If evidence is missing or cannot be verified, do not assume the claim is true.

## Check execution

1. Run each check in the order listed in rubric.md.
2. Assign pass, fail, or unclear using that check's pass condition.
3. Mark a check fail when the evidence contradicts the requirement. Use unclear when the available evidence cannot establish whether the requirement is met.
4. Do not fail a PR solely because it has an honestly disclosed, non-blocking limitation. Apply the rubric's requirements to decide whether the limitation affects the result.
5. Include one short, specific piece of evidence for every check. Use the gathered evidence instead of re-reading the whole package unless something needs clarification.

## Verdict assembly

1. Apply the verdict rule in rubric.md. Accept only when every required check passes; otherwise reject. Treat unclear as a failure when the required condition cannot be verified.
2. Include every check's name, grade, and one-line evidence in the final JSON. Use the check names from rubric.md exactly.
3. If the verdict is reject, identify the first failing required check in rubric order as the main reason. Quote the specific evidence that caused it.
4. If the verdict is accept, use the first required check in rubric order as the deciding check and state the evidence that supports its pass.
5. Ensure the JSON is valid and follows the exact output format in SKILL.md.