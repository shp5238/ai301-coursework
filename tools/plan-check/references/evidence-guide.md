# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

In an eval bundle, read the issue context and thread highlights for the reported behavior, the repro-evidence block for commands, controls, logs, and the earliest demonstrated failure point, and the candidate plan for its diagnosis and chosen intervention. In live mode, use the GitHub issue body and maintainer comments, the student's posted Unit 2 repro comment (or quoted house repro pack), and the diagnosis in `plan.md` and `comment.md`.

Good evidence connects the proposed cause to an observed artifact and respects controls that rule causes in or out. A bounded hypothesis is acceptable when the plan says how implementation or testing will verify it; a confident cause contradicted by the repro is not.

## Scope

In an eval bundle, compare the issue's requested outcome with the candidate plan's scope, exclusions, affected files or components, approach, and the promises in the plan comment. In live mode, compare the live issue and any maintainer scoping comments with the same parts of the drafts.

Good scope contains the smallest coherent change needed for the issue and explicitly leaves independent cleanup or follow-up work out. A plan is unbounded when it wraps the fix in migrations, redesigns, new options, broad platform support, or adjacent refactors whose necessity is not demonstrated.

## Executability

In an eval bundle, find the implementation layer, files or areas, sequence of work, and unresolved choices in the candidate plan; use repo facts only to verify named conventions or locations. In live mode, use the plan plus the repository tree and contributor documentation to verify that the named areas exist.

Good looks like a chosen approach with enough location and sequencing for another contributor to begin. The plan need not predict exact line numbers, but it cannot defer the core layer, architecture, dependency ownership, or basic approach until build time.

## Test plan

In an eval bundle, read the repro-evidence block for the failing command, input, artifact, and expected result, then read the candidate plan's test plan and expected observations. In live mode, use the posted reproduction evidence and the test section of the drafts; verify commands and paths against the repository when possible.

Good testing exercises the real changed path and names a result that flips from the reproduced failure to the requested behavior. A focused regression test or exact repro rerun is decisive; “run tests,” “try it manually,” or “should feel better” without an observable outcome is not.

## Honesty

In an eval bundle, read the candidate plan's risks, unknowns, alternatives, and deviations, then compare their certainty with the issue, thread, and repro evidence. In live mode, also compare post-build `## Deviations` with the actual diff when available.

Good work distinguishes verified facts from hypotheses, gives a way to resolve material unknowns, and records any difference between the posted plan and completed build. A direct plan may truthfully have no remaining material unknowns; invented certainty or a blank deviation record is not honest evidence.

## Comms

In an eval bundle, read thread highlights for explicit maintainer direction, prior art, ownership, or requested experiments; read repo facts for issue-template requirements, contribution policy, and AI-use disclosure rules; then compare them with both candidate drafts, especially the plan comment. In live mode, inspect the current issue thread, linked work, `.github` templates, `CONTRIBUTING` documents, and dedicated AI-policy files before reading the draft comment.

Good communication directly follows or thoughtfully distinguishes applicable maintainer direction, avoids racing active work, supplies requested fields, and makes any required AI disclosure. Silence in repository policy creates no invented requirement, but an explicit policy applying to issue comments must be followed.
