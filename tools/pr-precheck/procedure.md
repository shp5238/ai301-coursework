# Procedure: how this tool grades a PR package

<!--
THIS IS THE PART YOU WRITE (second week running for the procedure).
Week 3 you wrote these steps for a plan package; this week the graded
object is a PR package, and the read that matters most is a
side-by-side: the diff against the plan, the evidence against the test
plan, the description against both. Your week-3 procedure is the
pattern; do not paste it unchanged, because its read order was built
for a different object.

Your rotation is the design brief again, and this week friction routes
three ways: a stall on WHAT to decide is a rubric gap, a stall on
WHERE to look is a procedure gap (this file), and a stall on what the
tool even reads or outputs is a frame gap (your SKILL.md). A complete
procedure lets someone who has never seen a PR package before grade
one exactly the way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
plan's scope pair before opening the diff, and list the files the plan
names" is a step; "understand the change" is a wish.
-->

## Read order

1. In live mode, read `scope.md`, confirm the PR's base repository is
   the configured repository, and record its house rules. Stop without
   grading for a placeholder repo or an out-of-scope PR. Read the
   voice guide now but do not use it to change rubric grades by itself.
2. Read `rubric.md` and list its checks in table order, their weights,
   the verdict rule, and the treatment of `unclear`. Read the evidence
   guide and create one evidence worksheet row per check.
3. Read the issue and thread before candidate-authored text. Record the
   requested outcome, reproduction, constraints, maintainer direction,
   and known ownership or prior work.
4. Read repository facts next: the PR template, contributing rules,
   required checks or artifacts, and any AI-use policy.
5. Read the plan context before the diff. Record the original scope,
   exclusions, named files and behaviors, test plan, and every recorded
   deviation. This order prevents the completed code from silently
   redefining what was promised.
6. Read the candidate diff and commits. Inventory every changed file
   and material hunk, separating implementation, regression tests,
   documentation, and possible debris.
7. Read test evidence. Record each exact command or action, input,
   environment where relevant, before result, after result, expected
   result, control, and repository-check outcome.
8. Read the title and description last. Record every claim about issue
   linkage, scope, implementation, tests, limitations, template items,
   and AI assistance so each can be checked against earlier evidence.

## Evidence gathering

1. Build a plan-to-diff matrix. Put each planned file, behavior, and
   exclusion on one side and the implementing diff hunks on the other.
   Add every diff hunk that has no planned counterpart, then see
   whether a specific deviation note authorizes it. Mark promised work
   with no implementing hunk and whether the plan and description both
   disclose its deferral.
2. Build a description-to-diff claim list. For each claimed change,
   test, changelog/docs update, or "exactly as planned" assertion,
   point to the confirming artifact or record the contradiction.
3. Map every distinct completed-scope failure mode and every plan test
   case to the supplied evidence. Record whether it exercises the
   changed path, shows an observable before and after (or an explained
   equivalent), states the expected outcome, and covers controls or
   multiple failure modes the plan names. Treat a precise observation
   backed by a named passing regression test as evidence even without a
   full transcript. For repeated same-shape implementations, record
   whether one representative before/after, visibly identical diff
   interventions, and the reported suite jointly cover the siblings;
   do not demand duplicate transcripts merely because the same fix is
   applied in more than one method.
4. List every repository-required and plan-promised check. Beside it,
   record the exact reported command and outcome. Preserve honest
   failures, skips, and "no tests ran" results and record the supplied
   explanation and impact; absence is not the same as failure.
5. Inspect each material diff hunk for debug statements, dead helpers,
   suppression annotations, commented-out attempts, TODOs, repeated or
   formatting-only churn, generated noise, and drive-by edits. Record
   the smallest decisive line or hunk and whether any apparent
   refactor is necessary to the fix.
6. Translate each explicit template, contribution-policy, maintainer,
   and AI-disclosure ask into a requirement-to-artifact row. Record the
   description text or diff artifact that satisfies it; do not create
   requirements absent from the repository facts. In eval mode, mark
   every candidate as AI-assisted; if the stated policy requires all AI
   use to be disclosed, record a missing disclosure as unmet rather
   than assuming the package used no AI.
7. In live mode, compare the title and description with the voice guide
   separately. Record violations for the summary without adding a new
   rubric failure unless an existing check's condition also fails.

## Check execution

1. Execute checks once, in rubric-table order, using the completed
   worksheet rather than a general impression of the PR.
2. For each check, apply only its written pass condition and assign
   `pass`, `fail`, or `unclear`. Assign `fail` when the evidence shows
   the condition is not met. Assign `unclear` only after every named
   location has been inspected and the deciding fact remains absent or
   unverifiable.
3. Write one concise evidence line per check. When a comparison decides
   the grade, name both sides: for example, the plan's promised file
   and the missing diff hunk, or the required repro and the unrelated
   command actually run.
4. Do not let a strong fix compensate for missing decisive tests,
   debris, silent drift, or an explicit policy violation. Conversely,
   do not fail merely for brevity, imperfect commit messages, an
   honestly reported check failure, or a disclosed and recorded scope
   reduction when the check's outcome condition is met.
5. Once all evidence named by a check is in its worksheet row, grade it
   without rereading unrelated prose. If this procedure or the guide
   fails to locate required evidence, grade the affected check
   `unclear` and identify the procedural gap.

## Verdict assembly

1. After every check has a grade, apply the rubric rule: accept only if
   all required checks pass; otherwise reject. Count required
   `unclear` as rejecting and never allow a preferred check to change
   the verdict.
2. Present a short summary in rubric order with each check's grade and
   decisive evidence. For a rejection, identify the first failed or
   unclear required check in rubric order as the primary blocker, then
   retain every additional failing check rather than hiding it.
3. In live mode, append voice-guide notes after the rubric summary and
   state that they are non-gating unless they overlap a rubric failure.
4. Include every check once in the JSON array, in rubric order, using
   the same grade and one-line evidence as the summary. Use the PR URL
   in live mode or the bundle id in eval mode.
5. Validate the JSON, emit it in the contract's fenced block with the
   binary verdict, and write nothing after the closing fence.
