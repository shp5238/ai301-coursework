# Evidence guide: where evidence lives in a PR package

<!--
THIS IS THE PART YOU WRITE (third week running: the map stays in your
hands). Your tool uses this guide as its map: for every kind of
evidence a rubric check names, this file says WHERE to find it in a PR
package and WHAT GOOD LOOKS LIKE when you do.

The four families below are the harness's failure categories under
the names the eval README uses: plan fidelity = silent-drift, test
evidence = not-tested, diff quality = unreviewable, standards and
comms = standards-wall. A package that fails none of them is a
clear-accept. Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the plan-context block's scope pair and test
  plan, the candidate PR's diff, commits, description, or
  test-evidence section, the repo-facts block's template asks and
  stated policy). In live mode (where in your working copy and on
  GitHub: your plan.md and its deviation notes, your branch's diff,
  your draft title and description, your captured test output, the
  repo's PR template and CONTRIBUTING.md).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("every changed file falls inside the
  plan's stated boundary or a deviation note") over adjectives ("the
  diff is clean").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts three ways: your
procedure says WHEN to gather each family, this guide says WHERE, and
your SKILL.md says the tool reads both. Write the map you wish your
executor had.
-->

## Plan fidelity (harness category: silent-drift)

In an eval bundle, use the plan-context block for the accepted scope,
exclusions, named files, promised behavior, test plan, and deviation
notes. Compare those facts with the candidate diff and commits, then
compare both with the title and description. In live mode, read the
same facts from `plan.md`, including `## Deviations`, compare them with
`git diff main...HEAD`, and verify every claim in `pr_draft.md`.

Good evidence maps each material hunk to the plan or a specific,
reasoned deviation and maps each plan promise to either an implementing
hunk or a disclosure in both the deviation record and PR description.
Silent drift includes extra features or cleanup with no authorization,
missing planned work that is still claimed complete, and description
claims for tests, docs, or behavior the diff does not contain. A
recorded, honestly restated scope reduction is not silent drift.

## Test evidence (harness category: not-tested)

In an eval bundle, read the plan context's reproduction and test plan,
then the candidate test-evidence section and any testing claims in the
description. Use repo facts for required repository checks. In live
mode, compare the Unit 2 reproduction and test plan in `plan.md` with
the exact outputs in `test_evidence.md`, then verify that `pr_draft.md`
reports them faithfully.

Good evidence identifies the command or action, input, changed path,
observable before failure, expected after behavior, actual after
result, and relevant control for every distinct delivered failure
mode. A precise observation backed by a named passing regression test
is evidence even if the full console transcript is omitted. When the
same intervention is repeated in sibling methods, one representative
before/after may cover them if the diff visibly applies the identical
fix and the reported suite covers the siblings. Evidence also names
each applicable repository check and its real outcome. A shown failure
or expected no-tests result is evidence when explained honestly;
"tests pass," an unrelated control, an unchanged path, or a missing
distinct planned failure mode is not decisive proof.

## Diff quality (harness category: unreviewable)

In an eval bundle, inspect every material hunk in the candidate unified
diff and use the commit list as supporting context. In live mode,
inspect every committed change in `git diff main...HEAD --stat` and the
full three-dot diff; do not substitute the working-tree diff.

Good looks like a reviewer being able to see the bounded fix,
regression coverage, and required documentation without unrelated
noise. Debris includes debug prints, commented-out experiments, dead or
suppressed helpers, stale TODOs, duplicated or re-indented blocks,
formatting-only churn, generated noise, and drive-by cleanup. A local
refactor is acceptable only when the change itself shows it is needed
to deliver the fix. Weak commit messages may be mentioned, but they do
not make a clean diff unreviewable.

## Standards and comms (harness category: standards-wall)

In an eval bundle, read repo facts for PR-template sections and
checklists, contribution instructions, required tests or changelog/docs
artifacts, and AI-use policy; read thread highlights for explicit
maintainer direction. Locate compliance in the candidate description,
diff, and test evidence. In live mode, inspect the issue thread,
`.github/PULL_REQUEST_TEMPLATE.md`, `docs/CONTRIBUTING.md` or the
repository's equivalent contributing file, and any linked policy, then
compare them with `pr_draft.md`, the diff, and `test_evidence.md`.

Good means every explicitly applicable ask has substantive evidence:
required sections and issue linkage are present, checklist claims are
true, required artifacts exist or have a justified N/A, maintainer
direction is addressed, and a required AI-use disclosure is specific
and in the contributor's own words. In eval mode, every candidate is
treated as AI-assisted, so a policy requiring disclosure of any AI use
is satisfied only by an actual disclosure in the candidate text; do not
infer non-use from silence. Do not invent requirements where policy is
silent. Empty headings, untouched boilerplate, a false check, or
omission of an explicit disclosure or template requirement is a
standards wall. Description-versus-diff contradictions remain plan
fidelity problems even when the prose is polished.
