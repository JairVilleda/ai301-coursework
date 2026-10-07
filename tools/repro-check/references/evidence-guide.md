# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives:**  
In the `Environment:` line at the top of the candidate repro report. Compare it with the issue's stated environment and the repo-facts `bug reports:` requirement.

**What good looks like:**  
The environment includes the OS, tool/version, and any configuration or driver that matters to the issue. If the run uses a different version, branch, build, OS, or configuration than the issue or repo requires, the report clearly identifies that difference as a limitation.

## Steps

**Where it lives:**  
In the `Steps:` section or numbered steps of the candidate repro report. Include the stated starting state, commands, inputs, flags, configuration, and required dependencies.

**What good looks like:**  
A stranger should be able to start from the stated starting point and follow the steps to reproduce the reported result without guessing or using missing information. The steps should use the issue's actual trigger. Required flags, setup, configuration, and other dependencies should be included, and the steps should not depend on private or unavailable material.

## Behavior shown

**Where it lives:**  
In fenced output or log blocks, screenshots, or other concrete artifacts in the candidate repro report. Compare the observed result with the issue description and relevant thread highlights. Use `Expected:` and `Actual:` lines to help interpret the artifact.

**What good looks like:**  
The artifact shows the specific behavior described by the issue, such as the relevant error, output, state, exit code, crash, or other symptom. Statements like "verified" or "confirmed" are not evidence by themselves. For a cannot-reproduce report, look for the attempted trigger, its result, and an explanation of what differed from the issue's conditions.

## Honesty

**Where it lives:**  
In the candidate claim comment and repro report, together with the artifacts that support their statements.

**What good looks like:**  
The written outcome matches what the evidence actually shows. A cannot-reproduce result is good when the attempt and result are shown honestly. A claim of reproduction is not supported when the evidence is missing, shows a different behavior, or does not justify the level of certainty in the wording.

## Comms

**Where it lives:**  
In the candidate claim and repro comments, compared with the `Repo facts` contribution policy, bug-report requirements, and AI-use policy. Also compare the claim with the issue it refers to.

**What good looks like:**  
The comments follow the repo's stated requirements and include any required AI-use disclosure. The claim refers to the specific issue and says what will be investigated or reproduced. Avoid guarantees, deadlines, reservation requests, or generic boilerplate that could be posted on any issue.