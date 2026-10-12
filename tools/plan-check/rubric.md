# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis | The plan's stated cause compared with the repro evidence and steps. | The cause matches what the reproduction shows and is supported by the evidence. | required |
| Fix approach | The plan's proposed change compared with the reproduced bug and its cause. | The change addresses the cause instead of just hiding the symptom or changing unrelated behavior. | required |
| Scope | The plan's scope, files to change, and exclusions. | The changes are limited to what is needed to fix the bug, without unrelated work. | required |
| Implementation steps | The plan's approach and the relevant repository facts. | Another developer could understand where to start and what needs to change. | required |
| Test plan | The plan's test steps and expected results compared with the repro evidence. | The test checks the real bug and has an observable result that shows whether the fix worked. | required |
| Risks and unknowns | The plan's stated risks and assumptions compared with the available evidence. | Important unknowns are acknowledged instead of being presented as facts. | preferred |
| Thread and conventions | The plan comment compared with the issue thread and the proposed changes compared with repository conventions. | The comment addresses relevant discussion, and the changes follow known repository requirements and conventions. | required |

## Verdict rule

Accept if every required check passes. Reject if any required check fails. Preferred checks do not affect the verdict. An unclear result counts as a failure for required checks but does not cause rejection on its own for preferred checks. Only use the specified evidence to make a decision.
