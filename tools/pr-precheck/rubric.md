# Rubric: is this pull request ready to submit?

<!--
THIS IS THE PART YOU WRITE (fourth week running; this is the rubric's
final form in the sandbox). Your frame in SKILL.md executes whatever
checks you define here, via your procedure.md. It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the diff read against the plan's scope, the test
     evidence read against the plan's test plan, the description read
     against the diff, the repo-facts block's template asks) or a
     location from your references/evidence-guide.md. "The PR" is not
     a source; "the diff's changed files read against the plan's
     stated boundary" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself
     (does the diff fall inside the plan plus its deviation notes? is
     the claimed evidence observable?), never the write-up's shape
     (how long the description is, how many commits there are).
     Structure-shaped checks are what make graders disagree with
     themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (submit) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. State the `unclear`
   treatment explicitly: the frame here is YOUR SKILL.md, so a rubric
   that stays silent is only covered if your frame's grading
   discipline says what happens (the contract's own default is that
   an unverifiable claim fails).

Cover what actually gets bad PRs submitted. The failure families the
lecture named ARE the harness's scoring categories, same names as the
eval README: silent drift (the diff silently does more or less than
the posted plan, or the description claims fidelity the diff
contradicts), not tested (the evidence proves nothing observable, or
the repo's own checks were never run), unreviewable (debris or
unrelated hunks bury the change), and standards wall (the repo's
stated template and disclosure asks are ignored). Your evidence
guide's four headings map onto these one to one (plan fidelity =
silent drift, test evidence = not tested, diff quality =
unreviewable, standards and comms = standards wall), and the category
floor is scored on exactly these names plus clear accept. A rubric
that ignores a category will fail the eval packages built around
that category. And remember the honest-outcome
rule, fourth week running: a PR that honestly discloses a shortfall
can be ready; a rubric that equates "less than everything" with
"hold" fails the set.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | Compare the plan-context scope, exclusions, promised files and behaviors, and recorded deviations with every changed file and material hunk in the diff; compare both with the title and description's claims. | Pass when every material diff change is authorized by the original plan or a specific deviation note, every planned behavior omitted from the diff is explicitly deferred or explained in both the plan/deviation record and description, and the description neither claims work absent from the diff nor hides extra work. An honestly disclosed, coherent reduction of scope may pass; an unrelated addition or silent over- or under-delivery fails. | required |
| targeted-proof | Compare the plan's test plan and reproduction evidence with the candidate test-evidence section, including commands, inputs, before/after artifacts, controls, and expected results. | Pass when the evidence observably exercises the changed path and demonstrates the before failure and after outcome for every distinct failure mode still in the completed scope. A precise reported observation plus a named passing regression test is evidence even when its full console transcript is not pasted. One representative before/after may cover repeated same-shape implementations when the diff shows the identical intervention and the reported suite covers them. An equivalent decisive artifact may replace an impractical literal rerun if the package explains the equivalence. Generic assurances, testing only an unchanged control, or silently omitting a distinct planned failure mode fails; a behavior explicitly deferred in the recorded plan deviation and description is no longer part of the completed scope. | required |
| repo-checks-reported | Compare the repo-facts contribution policy and template testing asks, plus the plan's promised regression checks, with named commands and outcomes in the test-evidence section and description. | Pass when every applicable repository check and promised regression check has a reported outcome. A failure, skip, or expected "no tests ran" may pass when it is shown honestly, its cause and readiness impact are explained, and it does not invalidate the targeted proof. "Tests pass," "tested locally," or silence without identifying the applicable check fails. | required |
| diff-reviewable | Inspect the unified diff's material hunks and changed files, using the commit list only as supporting context, for debug output, dead or suppressed code, commented-out attempts, TODO debris, duplicated/reformatted lines, generated noise, or unrelated cleanup. | Pass when the intended change and its tests are directly reviewable and no material hunk is debris or unrelated to the bounded change. Necessary local refactoring may pass when the diff shows why the fix requires it; formatting churn, drive-by edits, retained experiments, and unrelated cleanup fail even when disclosed. Commit-message style alone never fails this check. | required |
| stated-standards-met | Compare the repo-facts PR-template asks, contributing instructions, explicit maintainer direction, and AI-use policy with the candidate title, description, diff, and evidence. | Pass when every explicitly applicable submission requirement is substantively satisfied: required sections or checklist facts are supplied, the issue is linked when requested, required tests or changelog/docs artifacts are present or honestly and reasonably marked inapplicable, explicit thread direction is engaged, and any required AI-use disclosure is present in the contributor's own words. In eval mode, treat every candidate package as AI-assisted: when repo facts require disclosure of any AI use, an absent disclosure fails even if the code and tests are otherwise ready. Do not invent a requirement from a silent policy, but boilerplate, omission, or an unsupported N/A against a stated ask fails. | required |
| reviewer-clarity | Read the title and description against the issue, plan, diff, test evidence, and disclosed limitations. | Pass when a reviewer can identify the problem, bounded solution, material changes, verification outcomes, and known limitations without the prose contradicting the artifacts. Minor terseness or style issues may be noted but do not fail an otherwise accurate package. | preferred |

## Verdict rule

Return `accept` only when every required check is `pass`. Return
`reject` when any required check is `fail` or `unclear`. Preferred
checks provide feedback and never change the verdict. Use `unclear`
only when all named evidence locations were checked but the decisive
fact cannot be verified; for a required check, `unclear` counts as
`fail` because an unverifiable submission is not ready.
