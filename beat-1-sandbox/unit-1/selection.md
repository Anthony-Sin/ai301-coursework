# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

````
All three URLs are in the scoped repo (`codepath/pathreview-ai301-fa26-s1`), so all three are valid candidates. Repo-level evidence gathered once and applied to each independently.

## Shared repo facts

- **maintainer-alive** — last default-branch commit `2026-09-16` by `Aburke225` (human, not a bot), 6 days before today. **pass**
- **repo-in-use** — `isArchived: false`, `pushedAt: 2026-09-16T21:48:27Z` (within 90 days). No releases ever published, which the rubric permits when pushes are fresh. **pass**
- **contribution-policy** — `docs/CONTRIBUTING.md` exists; zero occurrences of AI/LLM/Copilot/Claude anywhere in it, no `AI_POLICY.md`, no disclosure checkbox in the PR template. Silence passes. **pass**
- **maintainer-responsive** (preferred) — no maintainer *replies* in the 8 most recently updated issues, but `Aburke225` [COLLABORATOR] **authored** all three candidates on 2026-09-10/09-16, satisfying the check's second branch. **pass**

Only one PR exists in the entire repo across all states — `#74`, against issue `#60` — so none of the three candidates has a linked, open, or abandoned PR.

## Ranked read-out

**Accepted, in fit order:**

1. **#73 — README and `.env.example` disagree about which LLM API key to set.** The closest thing here to the "docs/UX papercut" the fit profile asks for: two named files, 1–2 hours, no Docker/Redis/Postgres needed to verify, and zero comments — completely uncontested. The smallest diff of the three, which leaves the exercise to be about the contribution workflow itself (clean branch, focused diff, review) rather than code comprehension.
2. **#68 — Keyword search raises `ZeroDivisionError` when the index is empty.** A bounded Python bug with wrong/right behavior stated and a ready-made `@pytest.mark.xfail` test to flip, so the test suite gives an unambiguous done signal — matches "comfortable running test suites."
3. **#62 — Health check references `settings.redis_host`.** Equally bounded, but the heaviest verification setup (`docker compose` with Redis and Postgres), and the same `/health` response carries a separate, unrelated Postgres failure to reason past.

**Rejected:** none.

Two things worth flagging:

- **#62 and #68 both carry live claim comments from course participants** (`ZJShown`, 2026-09-21, "I'm a TF... I'd like to take on this issue"; `yulijasso`, 2026-09-20, "I'd like to take this bug"), both detailed and both heading toward a PR. Under the Path Review house rule these do not block, and both authors show `author_association: NONE` — neither is a maintainer reserving the issue. #62 is the one judgment call in the set: a TF is course staff rather than a classmate, but they hold no maintainer badge and are claiming the issue for themselves, so I read it as a participant claim covered by the house rule, not a reservation. #73 needs no such reasoning — nobody has commented at all.
- **#62's thread ends on an open question** ("whether the fix should add `redis_host`/`redis_port` fields to `Settings`, or just have the health check build its client from `redis_url` directly"). This is not unsettled design under the rubric, because the maintainer's own opener already settles it: "it carries a single `redis_url`, which the probe should use instead."

```json
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by human Aburke225, 6 days before today (2026-09-22)."},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived: false; pushedAt 2026-09-16T21:48:27Z, within 90 days; no releases, which passes on fresh pushes."},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "One bounded docs change naming its files: 'Make the two files agree' across README.md and .env.example, est. 1-2 hours."},
      {"name": "nobody-on-it", "grade": "pass", "evidence": "No assignees, 0 comments, no linked PR (repo's only PR, #74, targets issue #60)."},
      {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has zero AI/LLM/Copilot mentions and no AI_POLICY file exists; silence passes."},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Issue authored by Aburke225 [COLLABORATOR] on 2026-09-16, within 90 days."},
      {"name": "newcomer-signaled", "grade": "pass", "evidence": "Labels: bug, good first issue, docs, tier-1."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by human Aburke225, 6 days before today (2026-09-22)."},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived: false; pushedAt 2026-09-16T21:48:27Z, within 90 days; no releases, which passes on fresh pushes."},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Single bug with stated wrong/right behavior ('index() shouldn't raise on an empty corpus either') and two named files plus an xfail marker to remove."},
      {"name": "nobody-on-it", "grade": "pass", "evidence": "No assignee and no linked or open PR; yulijasso's 2026-09-20 claim is a classmate comment [author_association NONE], which the Path Review house rule says does not block."},
      {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has zero AI/LLM/Copilot mentions and no AI_POLICY file exists; silence passes."},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Issue authored by Aburke225 [COLLABORATOR] on 2026-09-10, within 90 days."},
      {"name": "newcomer-signaled", "grade": "pass", "evidence": "Labels: bug, good first issue, rag, tier-1."}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/62",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Last default-branch commit 2026-09-16 by human Aburke225, 6 days before today (2026-09-22)."},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived: false; pushedAt 2026-09-16T21:48:27Z, within 90 days; no releases, which passes on fresh pushes."},
      {"name": "scope-fits-newcomer", "grade": "pass", "evidence": "Single bug with reproduction steps and a maintainer-stated direction in the opener: 'it carries a single redis_url, which the probe should use instead.'"},
      {"name": "nobody-on-it", "grade": "pass", "evidence": "No assignee and no linked or open PR; ZJShown's 2026-09-21 TF claim carries author_association NONE, so it is a participant claim under the house rule, not a maintainer reservation."},
      {"name": "contribution-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md has zero AI/LLM/Copilot mentions and no AI_POLICY file exists; silence passes."},
      {"name": "maintainer-responsive", "grade": "pass", "evidence": "Issue authored by Aburke225 [COLLABORATOR] on 2026-09-10, within 90 days."},
      {"name": "newcomer-signaled", "grade": "pass", "evidence": "Labels: bug, good first issue, api, tier-1."}
    ],
    "verdict": "accept"
  }
]
```
````

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

1. Full run (all 20 scored bundles, first draft of the rubric): **17/20** — `agreement: 17/20 scored items (bar: 18/20: below the bar)`. Disagreements: issue-01, issue-04, issue-19 — all gold `accept`, graded `reject` on `scope-fits-newcomer`.
2. `--only issue-01,issue-04,issue-19` after rewriting the scope check's fail triggers (distinguishing "parts of one task" from a tracker/umbrella): **3/3** — `agreement: 3/3 scored items`.
3. Full run: **19/20** — `agreement: 19/20 scored items (bar: 18/20: PASS)`. issue-01 flipped back to `reject` on `scope-fits-newcomer`; the other 19 agreed.
4. `--only issue-01 --out /tmp/issue01.json` diagnostic re-run to capture its check evidence: **1/1** — `agreement: 1/1 scored items` (graded `accept`; scope evidence: "Docs change naming its target files (new task page, manage-pkgs.rst, pip-interoperability.rst, new-features.md)").
5. Full run after strengthening the enumeration clause ("...still counts as one piece of work, however long the list of named edits is"; tracker defined as "a list of other issues, by number, meant to be picked up as separate work items or separate PRs"): **20/20** — `agreement: 20/20 scored items (bar: 18/20: PASS)`.
6. Final full run with `--save-run beat-1-sandbox/unit-1/eval-run.txt`: **20/20** — `agreement: 20/20 scored items (bar: 18/20: PASS)`, matching the agreement line in the committed `eval-run.txt`.

**Issue analysis**

`issue-09` (source `conda/conda#7617`, "conda config clear option"). Gold label: `accept`. My rubric's verdict: `accept` — every required check passed.

The deciding check was `nobody-on-it`, and it is the case that check's staleness clause exists for. The bundle's repo-facts line reads `this issue: assignees: none; linked PRs: conda/conda#11627 (closed)` — the one linked PR is closed, and my pass condition says "Closed or merged PRs alone do not block," so it does not count as a claim (it is also a single closed PR, under the `scope-fits-newcomer` trigger of "2 or more closed-unmerged linked PRs"). The thread holds one claim comment — MesaJonathan on `2022-01-20`: "I'd like to take a swing at this as my first open-source contribution. Does it need to be assigned to me?" — but the capture date is `2026-08-05`, over 1,650 days later, well past the 180-day window, so it is stale and does not block. The maintainer reply is an invitation, not a reservation: jakirkham (MEMBER) answered "Think you can just give it a try if you are interested." The remaining required checks pass on the repo facts: newest default-branch commits `2026-08-04` (within 90 days of capture), `last push to any branch: 2026-08-04` and `latest release: 26.7.0 (2026-07-31)` (within 12 months), `archived: no`, and a contribution policy that welcomes generative AI with review-and-understand conditions — conditions, not a ban. Scope passes because the ask is one bounded feature (`conda config --clear channels` emptying a list key) opened by a MEMBER carrying `good first issue` and `stale::recovered` labels; its 2018 open date is age, not abandonment — there is one lapsed claim, not "multiple lapsed claims."

**Check rationale**

Quoted verbatim from the `rubric.md` uploaded to `tools/issue-select/`:

> | nobody-on-it | Repo-facts "this issue:" line (assignees, linked PRs with per-PR state) plus the comment thread for claim comments and their dates. Live: the Assignees and Development boxes plus the thread; when the sidebar and the thread disagree, believe the thread. | All of: no assignee; no linked or thread-referenced pull request still open (in this repo or a fork); no live claim — a "I'll take this" / "working on this" / bot-claim comment dated within 180 days of the capture date whose author was not later unassigned and did not withdraw; and no maintainer comment reserving the issue for someone else. Claim comments older than 180 days with no visible follow-up are stale and do not block. Closed or merged PRs alone do not block. | required |

It is written this way because the three claim surfaces decay differently. An assignee is a live lock until removed, so any assignee fails. An open pull request is work in flight — a claim that never goes stale — so it fails at any age, in the repo or on a fork. A bare claim comment is the weakest signal: old "I'll take this" comments on good-first-issues are usually abandoned, so the check only counts claims inside a 180-day window where the author was not later unassigned and did not withdraw. 180 days sits between the live claims in the eval set (3 days on issue-18, 13 on issue-08, 86 on issue-03) and the stale ones (~900 days on issue-15, ~1,650 on issue-09). The maintainer-reservation clause exists for issue-03, where DanielNoord (COLLABORATOR) wrote "We are **not** looking for any other contributions other than @hamza-mobeen's PR" — an explicit statement that overrides every other signal regardless of dates.

**Trade-offs**

The 180-day staleness window gives up sensitivity to genuinely-live-but-old claims: a claim comment seven months old with no linked PR would grade as stale even if its author is still quietly working, and I could collide with their unannounced PR. I accept that miss for two reasons, both visible in the eval evidence. First, the other legs of the check catch real work that outlives the window: open linked PRs fail the check at any age, so issue-03 would still reject on `pylint-dev/pylint#10985 (open)` even if its "Working on this" comment (2026-05-11, 86 days before capture) had aged out, and a maintainer reservation comment blocks regardless of date. Second, the window is what flips issue-09 to `accept`: without the staleness clause, MesaJonathan's 2022-01-20 "I'd like to take a swing" would reject an issue a maintainer explicitly re-opened for takers ("Think you can just give it a try"), and gold agrees it should accept. Nothing else in the set moved when I added the clause — the nearest live claims sit at 3–86 days and the nearest stale ones at ~900+ days, so the exact threshold is not load-bearing on any other bundle; I confirmed that in the full 20/20 runs that followed the edit.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. **Fit to interests and time.** #73 is the closest match to what I said I want in my fit profile: a docs/UX papercut, not core internals. README and `.env.example` disagree about which LLM API key to set — I work in Python and small CLI tooling, so an env-var mismatch is something I can verify by reading two files, no services to stand up. The issue itself estimates the work as bounded (two named files), which fits the time I actually have this week, and keeps the unit's real exercise — clean branch, focused diff, responsive review — front and center instead of code comprehension.

2. **What the verdict caught vs. what I weighed beyond it.** The verdict correctly established the structural signals: the repo is alive (last default-branch commit 2026-09-16 by a human collaborator), the issue is maintainer-filed and bounded, nobody has an assignee/PR/reservation on it, and the contribution docs are silent on AI. What the rubric could not weigh: all three candidates came back `accept`, so the verdict alone did not pick. I weighed coordination cost — #62 and #68 both have detailed claim comments from course participants (a TF and a classmate), which the Path Review house rule says do not block but which still mean shared attention — versus #73's completely empty thread. I also weighed verification cost: #62's fix needs `docker compose` with Redis and Postgres to exercise the health check; #73 needs nothing but the repo.

3. **Anticipated claiming difficulty.** Low. #73 has zero comments, no assignee, and no linked PR — nobody has visibly moved on it. And even if classmates pile on later, the house rule means their claim comments do not block me: credit attaches to the PR I open, not to whether it merges. I will still post a claim comment early in Unit 2 as a courtesy signal, but I do not expect a race.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
