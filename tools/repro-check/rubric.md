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
| claim-is-specific | Read the issue title and described behavior, then the candidate claim comment. Compare what the claim names, what work it promises, and any asserted outcome or schedule. | Pass when the claim identifies the issue-specific behavior or component, promises an investigation and reproduction report, and does not assert an unperformed reproduction, promise a fix, or promise a completion date. Fail when it is generic enough to fit unrelated issues, claims evidence not yet gathered, or commits to a fix or deadline. If the claim comment is absent, grade `unclear`. | required |
| environment-matches-target | Read the issue's stated platform or version constraints and the repro report's environment record. Look for the operating system, relevant runtime/tool versions, dependency state when material, and an exact code revision, tag, branch plus commit, or other reproducible code state. | Pass when the environment record identifies the code state and every environment fact needed to interpret the result against the issue, and either matches the issue's target or explicitly explains a relevant difference. Do not require irrelevant version inventories. Fail when a missing or mismatched environment fact could change the observed behavior. If the issue gives no target and the report still records a reproducible relevant environment, pass; if the code state or a necessary environment fact cannot be determined, grade `unclear`. | required |
| steps-are-rerunnable | Read the repro report's setup and reproduction steps together with commands, fixture/input details, and the repository's documented setup prerequisites in the issue context or repo-facts block. | Pass when a stranger starting from the recorded code state can follow the stated prerequisites, commands, inputs, and actions through the trigger without guessing a material step. Established repository setup may be referenced precisely instead of recopied. Fail when a missing command, input, state transition, credential assumption, or setup dependency prevents rerunning the attempt. If the trigger path is not given, grade `unclear`. | required |
| evidence-shows-target-behavior | Read the issue's expected and reported behavior, then inspect the repro report's output excerpts, logs, screenshots, assertions, or other artifacts and the exact command or action that produced them. | Pass when the artifacts directly demonstrate the behavior the issue describes. Also pass an honest cannot-reproduce when the report makes a concrete, relevant attempt at the issue's trigger, shows the resulting target-facing artifact, and names any condition it could not reproduce or control; inability to prove that every hidden trigger precondition was achieved does not erase an otherwise evidenced attempt. Fail when the artifacts show only setup success, an adjacent failure, a different feature, a paraphrased conclusion without observable output, or output that contradicts the claimed target behavior. If no artifact links the attempt to the issue's behavior, grade `unclear`. | required |
| conclusion-matches-evidence | Compare every conclusion in the repro report with the recorded steps, environment, and artifacts. Include statements of reproduced, intermittent, fixed, or cannot reproduce. | Pass when the report states exactly what the evidence supports, including limitations and deviations, and distinguishes observation from inference. An evidenced cannot-reproduce passes. Fail when the report claims more certainty, scope, causation, or reproducibility than its artifacts establish, or hides a material failure or environment difference. If the conclusion is absent or cannot be reconciled with the artifacts, grade `unclear`. | required |
| repo-conventions-followed | In eval mode, read the repo-facts block's issue-template requests, contribution policy, and AI-use or disclosure policy, then both candidate comments. In live mode, inspect the issue template, CONTRIBUTING guidance, linked contributor docs, PR/comment templates when applicable, and dedicated AI-policy files, then the drafts. | Pass when the comments supply every convention that applies to issue claims or reproduction reports, including required AI-assistance disclosure, while avoiding disclosures or template fields the repository does not request. This course workflow is AI-assisted: when a repository requires disclosure of any AI use in issues or comments, absence of that disclosure fails even if the draft does not itself announce tool use. A silent policy or a policy that explicitly imposes no disclosure requirement on issue comments imposes none. Fail when an applicable required field, format, or disclosure is missing or contradicted. If a relevant known policy exists but its rule cannot be read, grade `unclear`. | required |

## Verdict rule

Accept only when every applicable required check passes. Reject when any
applicable required check fails or is `unclear`. In a claim-only live run,
the environment, steps, behavior, and conclusion checks are not yet
applicable and are excluded from the verdict exactly as `SKILL.md` directs;
`claim-is-specific` and `repo-conventions-followed` still gate the claim.
Preferred checks, if added later, may rank or improve a package but never
change its verdict.
