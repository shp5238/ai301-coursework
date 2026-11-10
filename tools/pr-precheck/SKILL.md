---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

<!--
THIS IS THE PART YOU WRITE, and it is the last one: the frame itself.
Weeks 1 through 3 handed you a working SKILL.md and you filled the
files behind it; this week the frame ships as headings, and you write
what it says. The frontmatter above and the section headings below are
fixed (CONTRACT.md's layout rule); the instructions under each heading
are yours. Write instructions to the tool, in the imperative, the way
weeks 1-3's frames spoke to you: what to read, in what order, what to
refuse, what to emit. Your executor in the rotation is the test: a
frame gap they hit (cannot tell what the tool reads, or how a verdict
gets assembled) is a missing sentence here.

One section is not yours: the JSON schema in "Verdict and output" is
reproduced from CONTRACT.md verbatim and may not be altered. Your
words decide everything around it.
-->

## The question

Answer exactly one question about exactly one pull-request package: is
this ready to submit? A package consists of one candidate title and
description, its commits and diff, its test evidence, and the plan it
claims to implement, all read against the issue, thread direction, and
repository standards. Grade one package per run. Do not review a
different artifact or invent readiness from general impressions.

## Inputs and modes

Choose the mode from the supplied input:

- In **live mode**, read the issue URL and its full thread; `plan.md`,
  including `## Deviations`; the committed branch diff produced from
  the working copy by `git diff main...HEAD`; the draft PR title and
  description in `pr_draft.md`; and the captured commands and outputs
  in `test_evidence.md`. Also read the repository's PR template and
  `docs/CONTRIBUTING.md` (or the repository's equivalent contributing
  file) for explicit standards. Treat the three-dot diff as the whole
  proposed change; do not grade uncommitted code. For a house-chain
  submission, use the supplied house issue, house repro pack, house
  plan, and branch in the same roles.
- In **eval mode**, read only the single supplied package bundle. The
  bundle's issue, thread highlights, repo facts, plan context,
  candidate PR, diff, commits, and test evidence are the whole world.
  Fetch nothing and read no outside files. Run every rubric check and
  apply the complete verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` before any package artifact. Apply its
repository boundary and house rules. Refuse to grade a PR whose base
repository is outside the configured repo. If the `Repo:` line is
still a bracketed placeholder, stop without grading and tell the user
to replace it with the section's Path Review repository; never guess.
Ignore `scope.md` entirely in eval mode.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after confirming scope and hold the
outgoing PR title and description against every applicable rule.
Report each violation in the readable summary by quoting the rule and
the conflicting draft text. A voice violation does not change the
verdict unless a check in `rubric.md` independently covers the same
outcome. Ignore `voice-guide.md` entirely in eval mode.

## Component reads

Read `rubric.md` for the complete list of checks, their pass
conditions and weights, and the verdict rule. Read
`references/evidence-guide.md` to locate each named evidence family.
Then execute `procedure.md` exactly as written to gather evidence,
grade checks, and assemble the verdict. If the procedure is silent on
a necessary step, report that gap and do not improvise a substitute.
If `rubric.md` contains no filled check or `procedure.md` contains no
operating steps, refuse to grade and identify the empty component.

## Verdict and output

Use only `accept` (ready to submit) or `reject` (hold). Before the
machine result, provide a compact per-check summary with the decisive
evidence for each grade and any live-mode voice notes. End with the
following syntactically valid fenced JSON block, in this exact schema
and order, and write nothing after the closing fence.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Name the concrete fact or short quote that decides every check;
  never use "looks good" or polish as evidence.
- Grade the actual diff, evidence, and compliance outcomes, not length,
  confidence, formatting, or commit-message elegance. Terse and
  complete passes; polished contradiction fails.
- Apply the rubric literally. If its stated pass condition produces an
  uncomfortable result, keep the result and surface the rubric tension
  rather than changing the grade ad hoc.
- Apply the procedure literally. Report a procedural gap rather than
  silently supplying a new step.
- Treat `unclear` exactly as the rubric's verdict rule directs. If that
  rule is silent, treat an unverifiable required outcome as a failure.
