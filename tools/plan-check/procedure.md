# Procedure: how this skill grades a plan package

## Read order

1. In live mode, read `scope.md`, confirm that the issue belongs to the scoped repository, and record the applicable Path Review house rules. Stop without grading if the repository is outside scope or the `Repo:` line is still a placeholder.
2. Read `rubric.md`, list every check in table order, and record the verdict rule and the treatment of `unclear` before reading the candidate drafts.
3. Read `references/evidence-guide.md` and make an evidence worksheet with one row for each rubric check and the package locations that check requires.
4. Read the issue context and thread highlights first. Record the requested outcome, constraints, maintainer directions, linked or active work, and repository conventions without letting the candidate plan redefine them.
5. Read the reproduction evidence next. Record the exact command or action, observed failure, controls, earliest demonstrated failure point, and expected behavior.
6. Read the candidate plan, then the candidate plan comment. Record the diagnosis, boundaries, files or areas, implementation steps, test observations, risks, unknowns, and any deviations. In live mode, also read `voice-guide.md` before assessing the comment's voice.

## Evidence gathering

1. For diagnosis, pair each causal claim in the plan with the reproduction fact that supports or contradicts it. Give controls and evidence showing where the failure first appears more weight than a thread guess.
2. For scope, list every promised change and compare it with the issue's requested outcome. Mark additions whose necessity is not shown, and record explicit exclusions that keep follow-up work separate.
3. For executability, extract the chosen implementation layer, named files or components, ordered actions, and any decisions deferred until build time. Record whether a new contributor can take the first implementation step from those facts.
4. For testing, map each targeted test or command to the reproduced input, real changed path, prior failing artifact, and expected post-fix observation. Record generic suite runs separately as regression coverage.
5. For honesty, list each risk, unknown, alternative, and deviation alongside the evidence available. Mark unsupported certainty and material decisions that remain open.
6. For communication, compare both the plan and comment with thread directions, prior-art or ownership signals, contribution requirements, templates, and AI-disclosure rules. In live mode, gather these from the issue and repository locations named in the evidence guide; in eval mode, use only the bundle.

## Check execution

1. Execute checks in rubric-table order using the completed evidence worksheet; do not substitute general impressions for a check's named evidence.
2. For each check, apply its pass condition literally and assign `pass`, `fail`, or `unclear`. Use `unclear` only after checking every named location and finding the deciding evidence genuinely absent; do not use it merely because the plan is concise.
3. Write one evidence line for every grade. Prefer the smallest decisive quote or fact, and name both sides when the grade depends on a contradiction between the plan and reproduction evidence.
4. Do not let polished formatting, length, or confidence compensate for a failed outcome. Conversely, do not fail a terse package when it meets the outcome stated by the pass condition.
5. Do not reread unrelated package sections once a check's complete named evidence has been gathered. If the guide or procedure leaves a required evidence source unmapped, grade the check `unclear` and note the procedure gap.

## Verdict assembly

1. Apply the rubric's verdict rule after every check has a grade: accept only if all required checks pass; otherwise reject. Convert required `unclear` grades to rejecting results as the rule directs, while preferred grades never alter the verdict.
2. Before the JSON, report each check's grade and decisive evidence in one short line. In live mode, add any voice-guide violation by quoting the broken rule, but do not change the verdict unless a rubric check also covers it.
3. Put the first failed or unclear required check's decisive evidence in the summary without hiding additional failures. Include every check in the JSON in rubric-table order.
4. Emit the skill's fenced JSON block with the package id or live issue URL and the binary verdict. Validate that the JSON is syntactically valid and write nothing after the closing fence.
