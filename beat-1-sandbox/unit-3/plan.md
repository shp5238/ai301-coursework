# Plan for issue #64: make the partial-overlap fixture genuinely partial

## Diagnosis

The relevance scorer is behaving correctly; the test fixture contradicts its own scenario. My Unit 2 reproduction showed that the query tokenizes to `django`, `framework`, `python`, and `web`, while the chunk contains all four tokens. Because `RelevanceScorer.score` divides the overlap count by the number of query tokens, the fixture produces full coverage and a score of `1.0`.

The decisive reproduced output was:

```text
>       assert 0.3 < score < 0.9
E       assert 1.0 < 0.9
Captured stdout: relevance_scored avg_score=1.0 chunks_count=1 query_len=4
```

This matches the issue's requested outcome: change the fixture so its overlap is genuinely partial rather than change correct scorer behavior.

## Scope

In scope:

- Update `test_query_with_partial_overlap` in `tests/unit/test_relevance_scorer.py` so the chunk omits at least one query token and still contains more than one matching token.
- Remove the issue-specific strict `xfail` marker once the corrected test passes.

Out of scope:

- Changes to `rag/evaluator/relevance_scorer.py` or its tokenization and scoring algorithm.
- Refactoring other relevance-scorer tests or changing their assertions.
- Adding new scoring features or changing score thresholds.

## Files

- `tests/unit/test_relevance_scorer.py`: correct the partial-overlap input and remove the resolved `xfail` marker.

## Approach

1. Change the chunk text from one containing all four query terms to one containing exactly three, which should produce a deterministic score of `0.75` under the current scorer.
2. Remove the `@pytest.mark.xfail(strict=True, ...)` annotation for issue #64, as required by the repository's seeded-bug workflow.
3. Inspect the diff to confirm that no production scorer behavior or unrelated tests changed.

## Test plan

1. Re-run the formerly failing target with `--runxfail`:

   ```console
   python -m pytest -p no:cacheprovider tests/unit/test_relevance_scorer.py::TestRelevanceScorer::test_query_with_partial_overlap --runxfail -q
   ```

   Expected after the fixture edit: the test passes, and direct inspection of the same inputs shows three of four query tokens overlap, producing `0.75` rather than `1.0`.

2. Run the complete relevance-scorer unit file:

   ```console
   python -m pytest -p no:cacheprovider tests/unit/test_relevance_scorer.py -q -rxX
   ```

   Expected: all 19 tests pass with no xfail or strict XPASS for issue #64.

## Risks and unknowns

The change is confined to one test fixture. The main risk is accidentally selecting text that still contains all four query tokens or too little overlap for the existing `0.3 < score < 0.9` assertion. I will verify the exact token intersection and score after editing. No production behavior is expected to change.

## Deviations

Nothing changed from the posted plan. The fixture now omits `web`, which gives the intended three-of-four token overlap and a score of `0.75`; the issue #64 strict `xfail` marker was removed, and the complete relevance-scorer unit file passes all 19 tests.
