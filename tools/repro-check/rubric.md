# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The `Environment:` line in the repro report, compared with the issue and the repo-facts `bug reports:` requirement. | The report records the OS, tool/version, and any relevant configuration or driver. If the issue or repo requires a specific version, branch, build, OS, or configuration, the run matches it or clearly calls out the difference as a limitation. A difference does not count as called out if it is presented as a new finding instead. | required |
| steps-rerunnable | The `Steps:` or numbered steps in the repro report, including the starting state, commands, inputs, flags, configuration, and required dependencies. | A stranger can follow the steps from the stated starting point to the reproduction attempt using only the information provided. The steps use the issue's actual trigger, including relevant commands, inputs, flags, and configuration. A changed trigger fails unless the change is clearly explained and justified. Required setup cannot be omitted, and the steps cannot depend on private or unavailable material. | required |
| behavior-matches-issue | Output, logs, screenshots, or other concrete artifacts in the repro report, compared with the issue and thread highlights. | The report contains concrete evidence of the reproduction result, and that evidence shows the specific behavior described by the issue, such as the relevant error, output, state, exit code, crash, or other symptom. Statements like "verified" or "confirmed" are not evidence by themselves. Evidence of a different or adjacent problem does not pass. For cannot-reproduce reports, the attempted trigger and result must be shown, along with the relevant difference from the issue's conditions. | required |
| outcome-honest | The claim comment and repro report, together with the evidence supporting them. | The comments do not claim more than the evidence shows. An evidenced cannot-reproduce result passes. A reproduction claim fails when the evidence is missing, contradicts the claim, shows a different behavior, or does not support a strong certainty claim. | required |
| comms-follow-conventions | The claim and repro comments, compared with the issue, repo-facts contribution/communication requirements, and AI-use policy. | The comments follow the repo's communication and contribution rules. If AI disclosure is required for issue comments, the comments include an appropriate disclosure. If disclosure is not required, its absence is not a failure. The claim identifies the specific issue and says what will be investigated or reproduced without guarantees, deadlines, reservation requests, or generic boilerplate. | required |

## Verdict rule

Accept if every required check passes. Any required failure means reject. Treat `unclear` as fail. Preferred checks never affect the verdict.