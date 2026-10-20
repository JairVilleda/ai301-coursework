# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Where to look: In eval mode, compare the plan's scope, boundaries, and documented deviations with the candidate PR's diff and description. In live mode, use plan.md, its deviation notes, git diff main...HEAD, and the draft PR title and description (for example pr_draft.md).

What good looks like: Every change fits the plan's scope or is explained in a documented deviation. The description accurately reflects what the diff changes. Changes outside the plan, missing planned changes without explanation, or unsupported claims indicate silent drift.

## Test evidence (harness category: not-tested)

Where to look: In eval mode, read the plan's test plan and the candidate PR's test-evidence section. In live mode, compare the test plan in plan.md with the actual command output recorded in the test evidence (for example test_evidence.md). Check the repository's applicable test requirements too.

What good looks like: Prefer the actual command and output. Observable before/after evidence should demonstrate the intended fix. A specific, named suite-pass statement or control result may support the assessment without full output; a generic claim that 'tests pass' is not sufficient. Report missing or unsuccessful required checks honestly.

## Diff quality (harness category: unreviewable)

Where to look: Inspect the candidate PR's diff and commit list in eval mode. In live mode, use git diff main...HEAD and the branch's commits.

What good looks like: The intended fix is clear, and unrelated edits or unnecessary code do not make it harder to review. Look for unrelated formatting changes, leftover debugging code, dead code, and commented-out blocks.

## Standards and comms (harness category: standards-wall)

Where to look: In eval mode, use the repo-facts section for the PR template's requirements and any stated contribution or disclosure policies. In live mode, read .github/PULL_REQUEST_TEMPLATE.md, docs/CONTRIBUTING.md, and any applicable repository policies. Compare those requirements with the PR title and description, including relevant maintainer instructions in the issue thread.

What good looks like: The PR addresses the repository's stated requirements and includes the requested information and disclosures. Boilerplate without the required details or ignored requirements indicates a problem. Whether the description's claims match the diff belongs under plan fidelity.