# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer Activity | Last 5 default-branch commits and recent issue discussion showing maintainer activity | Pass if there is evidence of maintainer activity within the last 90 days, such as a maintainer commit or meaningful maintainer response | required |
| Repository Activity | Default-branch commit history and repository archived status | Pass if the repository is not archived and has at least one commit within the last 90 days | required |
| Bounded Scope | Issue body and comment thread | Pass if the issue describes one specific, actionable task with a reasonably clear expected outcome, and there is no unresolved design/architecture discussion, umbrella/tracking scope, or evidence of repeated abandoned implementation attempts | required |
| No Active Contributor | Issue assignee, linked/open PRs, and issue comment thread | Pass if there is no current assignee, no open linked PR, and no clear evidence that another contributor is actively working on it | required |
| Contribution Policy | CONTRIBUTING.md, AI policy, contribution guidelines, AGENTS.md, and other repository-policy documents | Pass if the repository allows AI-assisted contributions. Requirements such as disclosure, testing, human review, understanding, and contributor responsibility are allowed; an outright ban on AI-assisted contributions fails | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept the issue only if all required checks pass.
If any required check fails, reject the issue.
If evidence is unclear, treat the check as failed