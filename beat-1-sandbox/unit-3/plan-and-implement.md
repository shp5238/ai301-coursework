# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

## Posted upstream

**GitHub username**

shp5238

**Plan comment**

[https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64#issuecomment-6228763720](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64#issuecomment-6228763720)

I plan to correct the fixture in `test_query_with_partial_overlap`, not the scorer. My reproduction showed that the query and chunk share all four query tokens, so the current scorer correctly returns `1.0`:

```text
assert 1.0 < 0.9
relevance_scored avg_score=1.0 chunks_count=1 query_len=4
```

I will update the chunk to omit one query term so it has genuine partial overlap, remove the issue #64 strict `xfail` marker once the test passes, and leave `RelevanceScorer` unchanged. I will verify that the target produces a middle-range score (expected `0.75`) and then run the complete `tests/unit/test_relevance_scorer.py` file, expecting all 19 tests to pass with no issue #64 xfail or XPASS.

## Your branch

**Branch**

`fix/64-partial-overlap-fixture`

**Evidence**

Before the fix:

```console
$ python -m pytest -p no:cacheprovider tests/unit/test_relevance_scorer.py -q -rxX
..x................                                                      [100%]
=========================== short test summary info ============================
XFAIL tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap - issue #64: relevance scorer 'partial overlap' fixture actually has full overlap
18 passed, 1 xfailed in 0.40s
```

```console
$ python -m pytest -p no:cacheprovider tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap --runxfail -q
F                                                                        [100%]
=================================== FAILURES ===================================
_____________ TestRelevanceScorer.test_query_with_partial_overlap ______________
>       assert 0.3 < score < 0.9  # Partial overlap should be in middle range
E       assert 1.0 < 0.9
----------------------------- Captured stdout call -----------------------------
relevance_scored avg_score=1.0 chunks_count=1 query_len=4
=========================== short test summary info ============================
FAILED tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap
1 failed in 0.19s
```

After the fix:

```console
$ python -m pytest -p no:cacheprovider tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap --runxfail -q
.                                                                        [100%]
1 passed in 0.22s
```

```console
$ python -m pytest -p no:cacheprovider tests/unit/test_relevance_scorer.py -q -rxX
...................                                                      [100%]
19 passed in 0.18s
```

```console
$ python -c "from rag.evaluator.relevance_scorer import RelevanceScorer; q='Python Django web framework'; c={'text':'Django is a Python framework for rapid development'}; s=RelevanceScorer(); print('query_tokens=', sorted(s._tokenize(q))); print('overlap=', sorted(set(s._tokenize(q)) & set(s._tokenize(c['text'])))); print('score=', s.score(q, [c]))"
query_tokens= ['django', 'framework', 'python', 'web']
overlap= ['django', 'framework', 'python']
relevance_scored avg_score=0.75 chunks_count=1 query_len=4
score= 0.75
```

## Eval iterations

**Run history**

1. Targeted smoke run (`pkg-02,pkg-06,pkg-20`): `agreement: 3/3 scored items`.
2. Final complete saved run: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Package analysis**

For `pkg-04`, the final rubric decided `reject`, matching the gold label `reject`. The issue thread says the owner isolated the culprit in `src/tui/light_windows.go`, posted a patched test binary, and asked for testing. The candidate instead proposed only documenting a workaround and did not address that direction. The required `thread-direction-followed` check therefore failed even though the workaround itself was concrete.

**Check rationale**

Final `thread-direction-followed` check, quoted exactly from the uploaded `rubric.md`:

> | thread-direction-followed | Read the candidate plan and plan comment against explicit maintainer direction, prior-art links, ownership claims, and requested experiments in the issue context or thread highlights. | Pass when the proposal follows, directly answers, or explicitly and reasonably distinguishes every applicable maintainer direction; it must not silently pursue a conflicting approach or race known active work. If the thread contains no applicable direction, pass. | required |

I made this check required because a technically bounded plan can still be unready when it ignores the maintainer's chosen direction or duplicates active work. The pass condition also permits a reasoned alternative instead of forcing blind agreement, and it explicitly passes when there is no applicable direction so quiet threads are not penalized.

**Trade-offs**

This check gives maintainer and ownership signals more weight than an independently workable proposal. It changes `pkg-04` to reject because the candidate silently substitutes a documentation workaround for the owner's requested code experiment, while `pkg-03` and `pkg-08` remain accepted because their plans engage existing work rather than racing it. The trade-off is that a contributor must spend plan space distinguishing a different approach when the thread already points elsewhere, but that coordination cost is preferable to posting a conflicting plan without acknowledgment.
