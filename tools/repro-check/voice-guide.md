# Voice guide: how I talk upstream

## Who I am in threads

I am a student contributor learning an existing codebase through a small,
bounded issue. I communicate what I actually ran and observed, and readers
can expect concrete commands, relevant environment details, and clear limits
on what I know.

## Rules I write by

### Rule: Promise the investigation, not the outcome

Before reproducing, I say what I will investigate and report back; I do not
promise a fix or a date I cannot guarantee.

- Wrong: "I'll fix this by tomorrow."
- Right: "I'll try the reported test case in my environment and post the exact result here."

### Rule: Lead with reproducible specifics

I name the concrete behavior, command, or component instead of posting a
generic claim or confirmation.

- Wrong: "I can take this and will look into it."
- Right: "I'll investigate the partial-overlap fixture in `test_query_with_partial_overlap`, run the reported pytest command, and share what I observe."

### Rule: Separate observation from explanation

I distinguish terminal output I saw from a possible cause I have not proved.

- Wrong: "The scorer is broken because the tokenizer is wrong."
- Right: "The test returned a score of 1.0; the fixture's full keyword overlap may explain that result, but I have not isolated causation."

### Rule: Make limits visible

I state relevant environment differences, incomplete attempts, and
cannot-reproduce outcomes rather than smoothing them over.

- Wrong: "Confirmed on the latest version."
- Right: "I could not reproduce this at commit `abc123`; the reported test passed on Python 3.12, so this result may differ from the original environment."

### Rule: Disclose assistance when required

I follow the repository's actual AI-assistance policy and make any required
disclosure specific and truthful.

- Wrong: "No need to mention tooling because I reviewed the output."
- Right: "I used an AI assistant to help organize the reproduction steps and verified every command and observation myself."

## Things I never post

- A promise to fix, merge, or finish by a particular date.
- A claim that I reproduced something when the shown artifact proves a
  different behavior.
- "Same as above" in place of evidence from my own environment.
- Guesses presented as root causes or maintainer decisions.
- Logs, screenshots, or generated text I did not inspect myself.
