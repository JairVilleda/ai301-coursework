# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| silent drift | Compare the diff with the plan's scope and documented deviations. Check the PR description's claims against the actual changes. | The changes match the plan, or differences are clearly disclosed. The description does not make claims that the diff contradicts. | required |
| not tested | Compare the test evidence with the plan's test plan. Check the commands and their actual output. | The plan's repro is demonstrated with observable before/after evidence, and the available test evidence identifies the tests or suites that were run. A named test-suite result or control result may be accepted as supporting evidence without full command output when the package provides a specific, credible statement of the result. Fail if the repro is not exercised, the evidence tests the unchanged path instead of the intended fix, a test-pass claim names no test or suite, or required plan checks are explicitly shown not to have been run. Apply the same standard consistently to all packages. | required |
| unreviewable | Inspect the changed files and hunks against the plan's stated scope. If available, also check the commits and look for leftover debug or dead code. | The intended fix remains easy to review. Unrelated changes, unrelated commits, or unnecessary code (including leftover debug or dead code) do not materially obscure it. | required |
| standards wall | Compare the PR title and description with the repository's PR template, contribution guidelines, and applicable disclosure requirements. In live mode, also use the house rules in scope.md. In eval mode, use only the supplied package and ignore scope.md. | The PR meets the repository's stated requirements (and, in live mode, the scope.md house rules) and includes required disclosures without making unsupported claims. | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. Treat unclear as fail when the evidence cannot verify a required condition. Preferred checks, if added later, never change the verdict. An honestly disclosed, non-blocking limitation does not automatically cause rejection; judge it against the required checks.
