# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

## Your identity upstream

**GitHub username**

shp5238

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64#issuecomment-6011058175

Hello! I'd like to work on the partial-overlap fixture in `test_query_with_partial_overlap`. I'll run the reported relevance-scorer test from the current course repository state, inspect the fixture's token overlap and score, and post my environment, exact commands, and observed output here before making any fix.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64#issuecomment-6011076920

I reproduced the partial-overlap fixture problem at course repository commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`.

Environment:

- macOS 15.6.1 (24G90), arm64
- Python 3.12.7
- pytest 9.1.1
- Code state: `codepath/pathreview-ai301-fa26-s3` `main` at `2f4e82f52efbcfcc57d65b3fa5348672163ca088`

Steps and observations:

1. From that checkout, I ran the test file with pytest's cache plugin disabled so the command would not write outside the isolated checkout:

   ```console
   python -m pytest -p no:cacheprovider tests/unit/test_relevance_scorer.py -q -rxX
   ```

   The suite recorded the target as the expected failure already associated with this issue:

   ```text
   XFAIL tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap - issue #64: relevance scorer 'partial overlap' fixture actually has full overlap
   18 passed, 1 xfailed in 0.27s
   ```

2. I reran only the target with the xfail marker disabled:

   ```console
   python -m pytest -p no:cacheprovider tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap --runxfail -q
   ```

   The test failed at the upper-bound assertion with the same value reported in the issue:

   ```text
   >       assert 0.3 < score < 0.9
   E       assert 1.0 < 0.9
   Captured stdout: relevance_scored avg_score=1.0 chunks_count=1 query_len=4
   1 failed in 0.21s
   ```

3. I inspected the exact fixture inputs using `RelevanceScorer._tokenize`. The query tokens were `django`, `framework`, `python`, and `web`; the overlap contained all four tokens, and `score(...)` returned `1.0`.

Expected: a fixture named partial overlap should omit at least one query term and produce a middle-range score satisfying `0.3 < score < 0.9`.

Observed: the chunk contains every query token, so the scorer correctly computes full keyword coverage (`1.0`) and the partial-overlap assertion fails when the xfail marker is disabled. This reproduces the fixture problem described in #64.

## Eval iterations

**Run history**

1. First complete run: `agreement: 18/20 scored items  (bar: 18/20: below the bar; category floor unmet: no match in disclosure)`.
2. Targeted disagreement and canary run: `agreement: 7/7 scored items`.
3. Final complete saved run: `agreement: 19/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

For `pkg-20`, the final rubric decided `reject`, matching the gold label `reject`. The package's reproduction evidence itself was strong, but its repo facts state: “All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance.” Neither candidate comment disclosed AI assistance. Because this course workflow is AI-assisted and the repository's policy explicitly applies to issues and comments, the required `repo-conventions-followed` check failed and the package was rejected.

**Check rationale**

Final `repo-conventions-followed` check, quoted exactly from the uploaded rubric:

> | repo-conventions-followed | In eval mode, read the repo-facts block's issue-template requests, contribution policy, and AI-use or disclosure policy, then both candidate comments. In live mode, inspect the issue template, CONTRIBUTING guidance, linked contributor docs, PR/comment templates when applicable, and dedicated AI-policy files, then the drafts. | Pass when the comments supply every convention that applies to issue claims or reproduction reports, including required AI-assistance disclosure, while avoiding disclosures or template fields the repository does not request. This course workflow is AI-assisted: when a repository requires disclosure of any AI use in issues or comments, absence of that disclosure fails even if the draft does not itself announce tool use. A silent policy or a policy that explicitly imposes no disclosure requirement on issue comments imposes none. Fail when an applicable required field, format, or disclosure is missing or contradicted. If a relevant known policy exists but its rule cannot be read, grade `unclear`. | required |

I made the AI-assisted-course assumption explicit after the first full run accepted `pkg-20` despite its repository's disclosure wall. The current form distinguishes a policy requiring disclosure in comments from a silent policy or one applying only elsewhere, so another grader can apply the same threshold.

**Trade-offs**

This required conventions check favors compliance over accepting an otherwise excellent reproduction. It correctly changed the disclosure canary `pkg-20` from accept to reject, while `pkg-07` continued to pass because its required disclosure was present. Its breadth can also be strict about other template requests: in the final run it rejected `pkg-05` for omitting `conda list` even though the gold label treated the supplied environment and direct parser evidence as sufficient. I accept that false-negative risk because missing an explicitly applicable repository requirement is costly, while the final evaluation still passed at 19/20 with every category represented.
