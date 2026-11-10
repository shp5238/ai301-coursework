# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/279

**Branch**

`fix/64-partial-overlap-fixture`

## Eval iterations

**Run history**

1. Full run: `20/20` scored items agreed; all five categories met the category floor. Final result: `PASS` at the `18/20` bar. This is the only eval run I performed, and it matches the final agreement line in `eval-run.txt`: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

I analyzed `pkg-01`. My rubric returned `reject`, matching the gold label `reject`. The package describes a strong, bounded parser fix with decisive before/after and ASAN evidence, but its repo facts say the pandas PR template requires “closes #xxxx with the issue number, tests added and passed, all code checks passed (pre-commit), type annotations added to new arguments, and an entry in the latest doc/source/whatsnew/vX.X.X.rst when fixing a bug.” The candidate description contains no `Closes #66657` line or required checklist, and the diff changes only `tokenizer.c` and `test_c_parser_only.py`, so it has no required whatsnew entry. My required `stated-standards-met` check therefore fails even though the implementation and testing are otherwise convincing.

**Check rationale**

Exact check from `tools/pr-precheck/rubric.md`:

> | stated-standards-met | Compare the repo-facts PR-template asks, contributing instructions, explicit maintainer direction, and AI-use policy with the candidate title, description, diff, and evidence. | Pass when every explicitly applicable submission requirement is substantively satisfied: required sections or checklist facts are supplied, the issue is linked when requested, required tests or changelog/docs artifacts are present or honestly and reasonably marked inapplicable, explicit thread direction is engaged, and any required AI-use disclosure is present in the contributor's own words. In eval mode, treat every candidate package as AI-assisted: when repo facts require disclosure of any AI use, an absent disclosure fails even if the code and tests are otherwise ready. Do not invent a requirement from a silent policy, but boilerplate, omission, or an unsupported N/A against a stated ask fails. | required |

I made this check outcome-based instead of requiring a particular amount or style of prose. It passes concise PRs when they substantively satisfy the repository's stated asks, while still rejecting technically strong changes that omit a required issue link, checklist fact, changelog artifact, or AI disclosure. The final two sentences prevent opposite errors: assuming no AI use when disclosure is required, and inventing requirements when the repository states none. That distinction let the rubric reject both standards-wall packages without penalizing clear accepts from repositories with different policies.

**Trade-offs**

Making `stated-standards-met` required means an otherwise correct, well-tested change can be held for submission-policy omissions; `pkg-01` is the concrete example. I accepted that trade-off because the tool answers whether a PR is ready to submit, not merely whether its code works, and missing an explicit required changelog or checklist makes it unready for that repository. I made no post-run changes or canary reruns because the first and only full run matched all `20/20` packages, including both standards-wall cases (`pkg-01` and `pkg-20`), while retaining all seven clear accepts.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
