# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

- **Where to look:** The plan's diagnosis and quoted repro evidence, plus the package's Repro evidence section and reproduction steps. In live mode, check the student's repro comment and the relevant issue discussion.
- **What good looks like:** The proposed cause explains what happened during the reproduction. The plan does not ignore or contradict the evidence.

## Scope

- **Where to look:** The plan's scope, files to change, and exclusions. Check the repo facts for any relevant rules.
- **What good looks like:** The changes are limited to what is needed to fix the bug. Unrelated work is left out unless the evidence shows it is necessary.

## Executability

- **Where to look:** The plan's approach, implementation steps, file names, and relevant repo facts.
- **What good looks like:** Another developer can understand where to start and what needs to change. The plan gives enough detail to get started without explaining every small coding step.

## Test plan

- **Where to look:** The plan's test steps and expected results, compared with the inputs, steps, and results in the repro evidence.
- **What good looks like:** The tests check the original bug and produce a clear result that shows whether the fix worked.

## Honesty

- **Where to look:** The plan's risks, assumptions, and unknowns. After implementation, check the Deviations section in plan.md.
- **What good looks like:** Important unknowns are stated instead of treated as facts. Any changes from the original plan are explained.

## Comms

- **Where to look:** The plan comment, issue context, thread highlights, and repo facts. In live mode, check the GitHub issue and relevant repository documentation or contribution rules.
- **What good looks like:** The comment matches the plan and addresses relevant discussion. The proposed changes follow known repository rules, including any AI-use disclosure requirements.