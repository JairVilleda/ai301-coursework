# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. Read the issue context and repo facts to understand the bug and any repository rules.
2. Read the repro evidence. Note what steps were followed, what happened, and what the evidence shows about the cause.
3. Read the candidate plan. Note the diagnosis, scope, files to change, approach, tests, and risks.
4. Read the plan comment and compare it with the plan and issue discussion.
5. Use the evidence guide to find the information needed for each check.

## Evidence gathering

1. For the diagnosis and fix approach, compare the plan's explanation and proposed change with the repro evidence.
2. For scope, note what will change, what will stay the same, and which files are involved.
3. For implementation steps, check whether the plan explains what to change and where to start.
4. For the test plan, compare the planned tests and expected results with the original reproduction.
5. For risks and unknowns, note any assumptions, unanswered questions, and possible problems.
6. For thread and conventions, compare the plan comment with the issue discussion and check the repo facts for relevant rules.
7. Keep track of the evidence you find for each check so you can explain your decision.

## Check execution

1. Grade each check in the order it appears in rubric.md.
2. Give each check a P (pass), F (fail), or ? (unclear).
3. Give a P when the evidence meets the pass condition and an F when it does not.
4. Give a ? when there is not enough evidence to decide. Do not guess.
5. Use the evidence named in the rubric and evidence guide. Do not judge a plan by its length, headings, or writing style.
6. Give a short reason for each grade and point to the evidence that supports it.

## Verdict assembly

1. Use the verdict rule in rubric.md to decide whether to accept or reject the plan.
2. Reject the plan if any required check fails or is unclear. Preferred checks do not decide the verdict.
3. Accept the plan only if every required check passes.
4. Report each check's grade and a short reason.
5. State the final verdict as accept or reject. If the plan is rejected, name the required check that caused it.