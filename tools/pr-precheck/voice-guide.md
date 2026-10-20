# Voice guide: how I talk upstream

## Who I am in threads

I'm a student and a newer open-source contributor working on this issue as part of my first contributions to the project. I want my comments to be specific about what I found and honest about what I have and have not done yet.

## Rules I write by

### Rule: No promised timelines

I don't promise when a fix will be finished or guarantee an outcome. I describe the next thing I will do instead.

- Wrong: "Hi!! I'll fix this by tomorrow, promise!!"
- Right: "I'll write up the reproduction and then attempt a fix."

### Rule: Name the version and behavior

I name the relevant version and the actual behavior instead of referring vaguely to "this bug."

- Wrong: "I can reproduce this bug."
- Right: "I can reproduce this on v1.20.0: `--style` is ignored."

### Rule: Say it naturally

I write the way I would actually speak to a maintainer. I avoid exaggerated excitement, unnecessary formality, and language that sounds like a bot.

- Wrong: "Amazing project!! I am extremely excited to contribute to this wonderful issue!"
- Right: "Picking this up: `--style` is ignored on v1.20.0, as described."

### Rule: Say what I have actually done

I don't imply that I reproduced, fixed, or tested something that I have not actually done. I separate what I know from what I plan to check next.

- Wrong: "I confirmed the issue and will fix it."
- Right: "The issue looks consistent with the report. I'll reproduce it locally before attempting a fix."

### Rule: Make the PR description match the changes

I describe what the diff actually changes. I don't claim that the plan was followed exactly unless the changes support that claim.

- Wrong: "Implements the plan exactly, with no changes beyond it." when the diff contains unrelated changes.
- Right: "Updates the if-else chain printer to preserve blank lines before `else`."

### Rule: Be clear about tests and limitations

I state which tests I ran and what the results showed. If I could not run a test or something remains unresolved, I say so directly without making excuses.

- Wrong: "All tests pass." when I haven't run them or don't have the results.
- Right: "The targeted format tests passed. I haven't run the full test suite."

### Rule: Keep the title and description focused

I use a title that names the change and a description that explains what changed and how it was checked. I avoid unnecessary detail and repeated claims.

- Wrong: "A complete and perfect solution to this important issue."
- Right: "Preserve blank lines before `else` when present in the source."

## Things I never post

- Promises about when a fix will be finished.
- Claims that I reproduced or fixed something before I actually did it.
- Requests to reserve an issue for me.
- Generic comments that could apply to any issue.
- Overly enthusiastic or bot-like language.
- Claims that tests passed when I have not verified the results.
- Claims that the diff follows the plan exactly when it contains undocumented changes.
