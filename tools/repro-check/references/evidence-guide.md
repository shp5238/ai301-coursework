# Evidence guide: where proof lives in a reproduction package

## Environment

**Where it lives.** In an eval bundle, compare the issue context and
repo-facts block with the repro report's environment or setup record. In
live mode, read the issue body and maintainer comments for supported
platforms or versions, then read the draft's environment paragraph and
commands. The repository's version files may clarify which runtime or
dependency versions matter.

**What good looks like.** The report names an exact code state (commit,
tag, or branch plus commit), the operating system, and only the runtime,
tool, or dependency versions that could affect this behavior. Those facts
match the issue's target, or the report calls out the difference so a reader
can interpret the result.

## Steps

**Where it lives.** In an eval bundle, use the repro report's prerequisites,
setup, numbered actions, commands, inputs, and fixture details; use repo
facts only for documented prerequisites. In live mode, compare the draft
with the repository's setup and test documentation and the issue's own
reproduction command.

**What good looks like.** A stranger can begin at the recorded code state,
satisfy the stated prerequisites, create the required input or state, and
run the trigger through to the observation without inventing a material
step. A precise link or command referring to established repository setup
is enough; generic instructions such as "set up the project" are not.

## Behavior shown

**Where it lives.** First identify the issue's expected behavior and exact
reported failure. Then inspect the repro report's terminal output, failing
assertion, log excerpt, screenshot, response payload, or other artifact,
together with the command or action that produced it. In live mode, the
posted draft must contain or directly link the evidence a thread reader is
expected to evaluate; unmentioned local files do not count.

**What good looks like.** The artifact exposes the same behavior, surface,
and trigger described by the issue. Passing setup output or a nearby error
does not prove the target. A cannot-reproduce report has good evidence when
the target command or action succeeds or behaves differently under the
recorded conditions and the relevant output is shown.

## Honesty

**Where it lives.** Compare the claim comment's promises and the repro
report's conclusion with the environment, steps, artifacts, warnings, and
failures elsewhere in the package. Pay attention to words such as
"reproduced," "always," "caused by," "fixed," and "cannot reproduce."

**What good looks like.** The claim promises only investigation and a
report. The final conclusion separates observations from hypotheses,
states material limits or mismatches, and uses no stronger certainty than
the artifacts support. A clear, evidenced cannot-reproduce is honest proof;
a confident reproduction of the wrong behavior is not.

## Comms

**Where it lives.** In an eval bundle, read the claim and repro comments
against the issue context and every applicable convention in repo facts,
including bug-report asks and AI-assistance or disclosure policy. In live
mode, inspect the issue template, CONTRIBUTING file and linked contributor
docs, dedicated AI-policy files, and relevant comment or PR templates.

**What good looks like.** The claim names this issue's concrete behavior
and next step rather than offering generic interest, and the repro comment
supplies the repository's requested diagnostic facts. Required disclosure
is explicit and accurate. When policy is silent, silence is acceptable;
inventing a disclosure requirement is not. Classmates' existing claims and
repros are interpreted under the Path Review house rules in `scope.md`.
