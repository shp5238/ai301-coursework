# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64

**Verdict output**

````text
Both repo evidence check out. Same-repo, both COLLABORATOR-filed, both `good first issue`+`tests`+`tier-1`, no assignee/PR/claim, no CONTRIBUTING/AGENTS/AI-policy files found (silent=pass), maintainer active (commits 2026-09-16, within window). Both accept.

**Rank:**
1. **#64** (relevance scorer fixture) — top fit. Single clear fix path ("fixture requires modification to create genuine partial overlap"), no ambiguity in approach.
2. **#63** (README scorer fixture) — accept but slightly less determinate: issue text offers two options ("extending fixture OR correcting assertion"), small extra judgment call vs #64.

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/64",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Owner/collaborator Aburke225 authored default-branch commits on 2026-09-16, within 12mo of today 2026-09-22"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "not archived, pushed_at 2026-09-16T21:50:20Z"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "one bounded outcome: fix test fixture so partial overlap is genuine, with exact repro command given"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; no comments; PR search for '64' in body returned 0 results"},
      {"name": "contribution-policy", "grade": "pass", "evidence": "no CONTRIBUTING.md, .github/CONTRIBUTING.md, or AGENTS.md found (404s) — silent"},
      {"name": "newcomer-signal", "grade": "pass", "evidence": "labels: bug, good first issue, tests, tier-1; maintainer-filed with named test file"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/63",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Owner/collaborator Aburke225 authored default-branch commits on 2026-09-16, within 12mo of today 2026-09-22"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "not archived, pushed_at 2026-09-16T21:50:20Z"},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "one bounded outcome: fix test fixture/assertion mismatch, exact repro command given"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: none; no comments; PR search for '63' in body returned 0 results"},
      {"name": "contribution-policy", "grade": "pass", "evidence": "no CONTRIBUTING.md, .github/CONTRIBUTING.md, or AGENTS.md found (404s) — silent"},
      {"name": "newcomer-signal", "grade": "pass", "evidence": "labels: bug, good first issue, tests, tier-1; maintainer-filed with named test file"}
    ],
    "verdict": "accept"
  }
]
```
````

## Eval iterations

**Run history**

1. Initial smoke test: `Initial result: 2/3`.
2. First complete scored run: `agreement: 16/20 scored items  (bar: 18/20: below the bar)`.
3. Targeted run of `issue-04,issue-09,issue-19,issue-20`: `agreement: 3/4 scored items`.
4. Targeted rerun of `issue-04`: `agreement: 1/1 scored items`.
5. Final complete saved run: `agreement: 20/20 scored items  (bar: 18/20: PASS)`.

**Issue analysis**

For `issue-04`, the final rubric decision was `accept`, matching the gold label `accept`. The issue describes one defect class—missing basic rule previews—and gives examples: “Including remove identity, fuse spiders, remove self loops, etc.” The maintainer filed it, labeled it `good first issue`, and left it unassigned with no linked PR. The final scope rule therefore treats the examples as instances of one coherent correction instead of separate independent outcomes.

**Check rationale**

Final `unclaimed` check, quoted exactly from the uploaded rubric:

> | unclaimed | In an eval bundle, inspect `this issue: assignees`, `linked PRs`, and the full comment thread for current work claims or PR references. In live mode, inspect the Assignees and Development boxes and the thread. Apply the Path Review house rule from `scope.md` in live mode. | In eval mode, pass if there is no assignee, no open linked or referenced implementation PR, and no current credible claim that remains active. Treat a claim comment as inactive when it is at least 12 months old and has no later evidence of ongoing work, open implementation PR, or assignment; it need not be explicitly released. Fail if an assignee, open implementation PR, or current active claim exists. In Path Review live mode, ignore classmates' claim comments as required by `scope.md`, but still fail an assignee or open linked implementation PR. If claim state cannot be determined from the available evidence, grade `unclear`. | required |

The 12-month threshold keeps a years-old expression of interest from blocking a first contribution forever while still rejecting evidence of current work. Assignment, an open implementation PR, or later evidence that work continues overrides the age threshold. The separate live-mode rule respects the course requirement that classmates' claim comments do not block a Path Review issue.

**Trade-offs**

This rule changed `issue-09`, the canary re-run with `--only`: its 2022 claim comment was more than four years old at capture time, with no assignee, no open linked PR, and no later evidence of ongoing implementation, so the final rubric accepted it. The trade-off is that a contributor who silently continues work for more than 12 months could be treated as inactive; requiring assignment, a PR, or recent evidence makes the rule reproducible instead of relying on speculation.

## Selection rationale

**Selection rationale**

1. Issue #64 fits my preference for small, bounded test fixes with clear expected behavior. It is labeled `tier-1`, identifies the test fixture to change, and should fit the available Unit 2 time better than a broader feature or architecture task.
2. The verdict correctly identified the active repository, absent assignment or PR, permissive-by-silence contribution policy, newcomer labels, and bounded outcome. Beyond the rubric, I compared the two accepted candidates and preferred #64 because it gives one direct correction, while #63 leaves a choice between changing the fixture and changing the assertion.
3. I expect claiming it to be straightforward because it had no assignee, comments, or linked implementation PR at grading time. Another student could still express interest before Unit 2, but the Path Review house rule says classmates' claims do not block participation, so I will follow the course claim process without treating that as exclusive ownership.
