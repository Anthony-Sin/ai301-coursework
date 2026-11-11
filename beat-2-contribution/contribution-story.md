# Contribution: CFP review all messages sorting links broken when not filtering

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Anthony Sinchi
**GitHub Username:** Anthony-Sin
**Issue:** https://github.com/emfcamp/Website/issues/1752
**Pull Request:** https://github.com/emfcamp/Website/pull/2394

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built the issue-scout over my unit-1 skill and ran one real scan**

Installed the scout (new SKILL.md, a real-repos scope, and my own
search-strategy.md with three `gh search issues` queries tied to my
fit profile), then ran one scan: 300 raw results narrowed to 266 by
my filters, top five graded. What fell short: my fewest-comments-first
ordering surfaced a repo that bulk-files analyzer findings (repowise)
twice in the top five — graded fine on checks, useless as a claim.
I noted the caveat in scan-notes.md rather than rewriting the filter,
since the direct grading of site picks is where the scout earns its
keep anyway.

**Unit 6: Installed the voice guard, gave the wild its scopes, wrote the repo-memory file**

Promoted my voice guide to `~/.claude/voice-guard/voice-guide.md` and
wrote the Upstream section (claims, questions, pings — a rule each with
wrong/right pairs). The guard's claim draft check caught my first
draft's missing check-in date, which is exactly the thing upstream
reads. Swapped repro-check and plan-check to the wild scopes, patched
the scout's scope check into `scope-feasible` with the difficulty-note
section (dated line in scan-notes.md). Wrote CLAUDE.local.md in my
emfcamp/Website clone: CONTRIBUTING.md is one page that just points at
IRC, so the file's real payload was the subsystem map — `messages()`
view, `messages.html` sort links, `sort_messages()`, the
`/admin/cfp-review` prefix, and the test-fixture login trick — which
saved me a second orientation pass when I came back to build the fix.

**Unit 7: Installed the ship-gate and wrote the manifest around a pre-existing failure**

Installed the ship-gate and wrote ship-manifest.md for emfcamp/Website
from its test.yml workflow: `uv sync`, `make check-syntax check-mypy`,
and pytest scoped to `tests/cfp_review tests/content`. The judgment
part: the full suite has `tests/volunteer/test_role.py::test_grouped_by_team`
failing identically on unmodified main (a seeded-data assertion), so
that row went into the manifest's excluded table with a dated reason
instead of either blocking my PR or being quietly dropped. Running the
gate on my branch caught nothing — which I verified the honest way by
having watched every check pass by hand first.

**Unit 8: Installed the PR monitor and wrote the playbook from real merge data**

Installed the monitor and wrote playbook.md: response rules, staleness
thresholds, nudge etiquette, walk-away criteria. The thresholds aren't
made up — I sampled merged PRs on emfcamp/Website and found outside
PRs merged same/next-day in July (event crunch) while the repo is quiet
off-season, so my nudge threshold is 14 quiet days. `--state` on my
real PR read it correctly (mergeable, 0 comments, QUIET under a day).
What fell short: a full drafting run costs a Claude call, and with a
zero-comment PR the "wait" move is obvious, so I ran state-only — the
playbook's real test comes when a review actually lands.

---

## Why I Chose This Issue

I searched two ways, the way the beat teaches. First the scout ran
one scan over GitHub with my strategy's three queries (python bug,
javascript bug, python documentation, all `good first issue`); the
top results were mostly tiny single-maintainer repos and one repo that
bulk-files analyzer findings — usable verdicts, unexciting claims.
Then I went to the Issue Selection site, filtered Python and
JavaScript, and shortlisted three: emfcamp/Website#1752 (CfP review
messages sorting broken without a filter), render-engine#1310 (broken
README link), and piscinajs/piscina#1029 (queueSize under AbortSignal).
My scout graded them: emfcamp accept/straightforward, and the other
two reject — render-engine on contribution-policy (the issue literally
carries a `No-AI` label and the maintainer said in the thread he
prefers no LLM help on docs issues, which I can't honestly ignore) and
piscina on scope-feasible (its described bug was already fixed by
merged PR #1030 — nothing left that the issue text asks for).

I chose emfcamp/Website#1752 because it fits my profile almost word
for word: Python, a bounded bug with the wrong and right behavior both
named in the issue, a runnable test suite, and maintainers who
deliberately labeled it `good first issue`. It also has real teeth for
learning: the bug lives at the seam between a Flask view and a Jinja
template, which is exactly the kind of "whose job is this" question I
wanted practice on. The honest read on the scout: it earned its keep
on the two rejects — the `No-AI` label check and the "is there work
left" check caught things I would have missed reading titles alone —
but its search ordering still rewards silence (fewest comments) over
fit, which is the thing I'd revisit before trusting it to pick for me.
Claim comment: https://github.com/emfcamp/Website/issues/1752#issuecomment-6787597383

**Toolkit**

- Tool: issue-scout — one strategy-driven scan plus direct grading of
  my three site picks
- What it produced: accept on emfcamp#1752 (straightforward), rejects
  on render-engine#1310 (contribution-policy) and piscina#1029
  (scope-feasible), all logged in scan-output.md
- Difficulties: the scan's fewest-comments ordering surfaced
  bulk-filed analyzer issues that pass checks but make poor claims
- What changed: the unit-6 scope patch (scope-feasible row +
  difficulty notes) replaced my unit-1 scope check; I'd next teach the
  ranking to penalize repos whose issue titles look machine-generated

---

## Understanding the Issue

**Problem Description**

On the CfP review "all messages" page, the table's sort links are
broken whenever the view is not filtered by proposal type: clicking
Date, From, Message Count, Proposal Title, or the unread-first link
takes you to an empty table instead of a sorted one.

**Expected Behavior**

Sorting the unfiltered messages table should reorder all proposals
that have messages — the same rows, new order.

**Current Behavior**

With no type filter the view substitutes `filter_type = "all"`, which
the template then injects into every sort link as `type=all`. The view
reads that back as a real filter (`Proposal.type == "all"`), which no
proposal has, so the sorted page shows zero rows — "All messages
(showing 0)".

**Affected Components**

`apps/cfp_review/base.py` (`messages()` view — filter handling) and
`templates/cfp_review/messages.html` (the five sort/unread links that
carry `type=type`). `sort_messages()` in the same file is not itself
broken — it never gets the rows.

**Toolkit**

- Tool: my repo-memory file (CLAUDE.local.md) — the scoped orientation
  map I wrote when I claimed the issue
- What it produced: the four places that matter (`messages()` view,
  the template's sort links, `sort_messages()`, the blueprint prefix),
  which I verified by reading each one before writing this section
- Difficulties: the map didn't mention the confidentiality-warning
  gate that redirects first-time admin sessions; hit it on my first
  test-client run and added it to the file
- What changed: updated CLAUDE.local.md's subsystem section with the
  confidentiality POST step

---

## Reproduction Process

**Environment Setup**

Linux (Arch), Python 3.14 via `uv sync --all-extras --dev`, Postgres 16
with PostGIS in Docker (`docker run -d -p 5432:5432 postgis/postgis:16-3.4`,
db `emf_site_test`). One deviation from the repo's docs: `config/test.cfg`
points SQLAlchemy at a `postgres` hostname that only exists inside
their docker-compose network, so I copied it to `config/test-localhost.cfg`
with a localhost URI and ran everything with `SETTINGS_FILE` set —
kept out of git via `.git/info/exclude`, never committed. Setup had one
real snag: the route lives under `/admin/cfp-review` now (the 2024 issue
says `/cfp-review`), which cost me a 404 before I checked the blueprint
registration, and first-time admin sessions get redirected to a
confidentiality warning you have to POST-agree through.

**Steps to Reproduce**

1. Seed two proposals (a talk and a workshop), each with one message
   to admin, and log in as a `cfp_admin` user through the test
   client's emailed login link.
2. `GET /admin/cfp-review/messages` — page shows "All messages
   (showing 2)"; inspect the sort links.
3. Follow a sort link: `GET /admin/cfp-review/messages?sort_by=date&type=all`.

**Reproduction Evidence**

- **Commit showing reproduction:** https://github.com/Anthony-Sin/Website/commit/1a809a6d2caa0638a1c2e299acb66d83f5996a65 (adds `tests/cfp_review/test_messages_sort.py`, which encodes exactly these steps; it failed on the unfixed view/template)
- **Screenshots/logs:** test-client output before the fix:

  ```text
  == GET /admin/cfp-review/messages (no filter) ==
  <h2>All messages <small>(showing 2)</small></h2>
  sort link: /admin/cfp-review/messages?sort_by=unread&amp;type=all
  sort link: /admin/cfp-review/messages?sort_by=date&amp;reverse=True&amp;type=all
  sort link: /admin/cfp-review/messages?sort_by=from&amp;reverse=True&amp;type=all
  sort link: /admin/cfp-review/messages?sort_by=count&amp;reverse=True&amp;type=all
  sort link: /admin/cfp-review/messages?sort_by=title&amp;reverse=True&amp;type=all

  == GET .../messages?sort_by=date&type=all ==
  <h2>All messages <small>(showing 0)</small></h2>
  has 'My test talk': False
  ```

- **My findings:** the bug is exactly as reported — every sort link
  carries `type=all`, and following one empties the table. The
  mechanism is two-sided: the view invents `"all"` as a placeholder
  filter value, and the template rebroadcasts it into links the view
  then takes literally. Fixing only one side leaves either an ugly URL
  or a footgun for hand-typed `?type=all` links.

**Toolkit**

- Tool: repro-check (with the wild scope) — graded my claim comment
  and this reproduction report against the issue
- What it produced: accept — the report shows the wrong behavior,
  names the mechanism, and someone else can run the same steps
- Difficulties: it flagged that my first draft's "steps" assumed the
  reader had an admin login; I rewrote step 1 to say exactly how the
  test client gets one
- What changed: the env-file workaround (`test-localhost.cfg` +
  `SETTINGS_FILE`) was my own addition to the report after its "could
  a stranger run this" check

---

## Solution Approach

**Analysis**

Root cause is a placeholder leaking across a boundary. In
`apps/cfp_review/base.py`, `messages()` does
`filter_type = request.args.get("type")` and, when it's falsy, sets
`filter_type = "all"` so the template can title the page "All
messages". But that same `type` variable is also interpolated into
every `url_for(..., type=type)` sort link in
`templates/cfp_review/messages.html`, producing `?sort_by=X&type=all`.
On the next request the view reads `type=all` as a genuine filter and
applies `Proposal.type == "all"`, which matches nothing. The sort
function is innocent — the rows are gone before it runs.

**Proposed Solution**

Fix both ends, each small: (1) the view treats `type=all` as
unfiltered, so the URL parameter can never silently empty the table —
this also covers hand-typed or stale links; (2) the template computes
`qs_type` (`none` when `type == 'all'`) so the sort/unread links stop
emitting the parameter at all, keeping URLs clean. Deliberately NOT
changing: the filter-by-type links (talk, workshop, etc. still pass
explicit types), `sort_messages()` itself, and the "all" display
title.

**Implementation Plan**

1. In `messages()`, change the filter condition to apply only when
   `filter_type and filter_type != "all"`; keep the `"all"` display
   fallback.
2. In `messages.html`, add `{% set qs_type = type if type != 'all' else none %}`
   and replace `type=type` with `type=qs_type` in the six sort/unread
   `url_for` calls (leaving the five explicit filter links alone).
3. Add `tests/cfp_review/test_messages_sort.py`: sorting with
   `type=all` still returns all proposals with messages; the rendered
   page contains no `type=all` link.

No deviations from this plan happened during the build — the diff is
exactly these three items.

**Toolkit**

- Tool: plan-check (wild scope) — graded plan.md plus my plan-comment
  draft against the issue and reproduction
- What it produced: accept — plan names the cause at the file level
  and states what it won't change
- Difficulties: it pushed on whether fixing "only the view" was
  enough; I split the fix into the two parts above because its
  "what about the ugly URL" objection was right
- What changed: the template half of the fix exists because of that
  objection — my first plan was view-only

---

## Testing Strategy

The observable proof is the reproduction run twice: (a) the two new
regression tests in `tests/cfp_review/test_messages_sort.py` —
`type=all` sorted requests return all proposals with messages, and the
rendered page contains no `type=all` link — failed on the unfixed code
(verified, output in Reproduction Evidence) and pass after the fix;
(b) the repo's own checks: `uv run --group dev make check-syntax` (ruff
format + ruff check: 221 files clean) and `make check-mypy` ("Success:
no issues found in 183 source files"), plus `pytest tests/cfp_review
tests/content` (13 passed, 14 skipped). In the full suite,
`tests/volunteer/test_role.py::test_grouped_by_team` fails identically
on unmodified upstream main — a seeded-data assertion my diff can't
touch — so it's recorded as excluded in my ship manifest rather than
chased.

**Toolkit**

- Tool: ship-gate (wrapping pr-precheck) — ran my manifest's checks
  plus the precheck on branch, plan, evidence, and PR draft
- What it produced: the manifest's pass table (sync, ruff, mypy,
  scoped pytest) green on my branch; the failing suite row documented
  as excluded with a dated reason
- Difficulties: deciding what to do about a failure that's real but
  not mine — the manifest's excluded table is the honest answer, and I
  verified it myself by running the test on a stash of clean main
- What changed: scoped the pytest row to the cfp_review surface after
  confirming the volunteer failure exists without my changes

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**2026-11-10**

Claimed emfcamp/Website#1752 on the Issue Selection site and posted my
claim comment on the issue. Spun up Postgres/PostGIS in Docker and
`uv sync`'d the repo; hit the `postgres` hostname snag in test.cfg and
made a localhost copy. First wrong turn: the issue says
`/cfp-review/messages` but the blueprint now mounts at
`/admin/cfp-review` — one 404 later I checked main.py's registration.

**2026-11-10**

Got the reproduction green-to-red: seeded a talk and a workshop with
messages, logged in an admin through the emailed link, POSTed through
the confidentiality warning (second wrong turn — forgot that gate
existed), and watched `?type=all` empty the table while the links in
the unfiltered page all carried it. Committed the failing regression
tests with the fix. Both halves of the fix in; new tests green, ruff
and mypy clean, scoped suite green; verified the one suite failure
(test_grouped_by_team) reproduces on clean main and wrote it into the
manifest's excluded table.

**2026-11-11**

Pushed `fix/1752-messages-sort-type-all` to my fork and opened
emfcamp/Website#2394 with the before/after output and the AI
disclosure. Ran the PR monitor `--state`: it read the PR as
mergeable, no checks reported, quiet.

**Toolkit**

- Tool: CLAUDE.local.md (repo memory) + ship-gate — the memory file
  carried the subsystem map into this session; the gate certified the
  branch
- What it produced: the fix commit (3 files, +76/−6), the PR
- Difficulties: none with the tools themselves; the wrong turns above
  were repo knowledge, which is now in the memory file
- What changed: nothing

---

## Pull Request

**PR Link:** https://github.com/emfcamp/Website/pull/2394

**PR Description:** "Fix CfP review messages sort links when not
filtering" — explains the `type=all` placeholder leak across view and
template, the two-sided fix, the new regression tests, includes the
before/after test-client output verbatim, lists the checks run (ruff,
mypy, scoped pytest) with the one pre-existing suite failure called
out as unrelated, and discloses the AI-assisted parts of my workflow.

**Maintainer Feedback:**

- 2026-11-11: none yet — PR opened today; the thread is quiet and
  that's a normal state, not a problem
- 2026-11-11: n/a — nothing to address yet

**Status:** Awaiting review

**Toolkit**

- Tool: ship-gate — its manifest checks ran before the PR opened; PR
  monitor — `--state` run after opening
- What it produced: gate pass on the branch; monitor read of
  "mergeable, 0 comments, QUIET"
- Difficulties: the gate can't see that a check it skipped is already
  broken upstream — that's on me to verify, which I did on clean main
- What changed: nothing yet; the playbook's 14-day threshold governs
  any nudge from here

---

## Learnings and Reflections

**Technical Skills Gained**

Flask blueprint/request-arg mechanics in a real production codebase —
how a query parameter flows view → template → next request, and how a
placeholder value becomes a lie the second it crosses a request
boundary. Standing up a foreign test stack (uv + Postgres/PostGIS +
the project's own fixture conventions) instead of expecting mine.
Writing regression tests with someone else's fixtures (module-scoped
app/db, login through the mailed link) rather than inventing parallel
ones.

**Challenges Overcome**

The test environment fought back twice — a config that assumes the
compose network's `postgres` hostname, and an admin flow gated by a
confidentiality POST — and both times the answer was a small local
artifact (a localhost cfg, an extra client POST) rather than a change
to the repo. The volunteer-suite failure was the scariest red until I
proved it fails on clean main; "verify it's not yours before you claim
it's not yours" is now a reflex. And the honest-tooling lesson from
the scout's rejects: a `No-AI` label and an already-merged fix are
facts you'd miss skimming titles — the checks exist precisely for that.

**What I'd Do Differently Next Time**

Check the blueprint's mounted prefix before trusting the issue's URL
(2024 path vs. today's `/admin/` prefix cost a debugging lap). Grade
site picks before scanning the wild, not after — the scan was good
practice but the site is where the claimable issues are. And run the
monitor's full drafting pass on a schedule rather than only when I
remember, since a review that lands on a quiet PR shouldn't sit.

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- https://github.com/emfcamp/Website/blob/main/.github/workflows/test.yml —
  the real contribution gate; CONTRIBUTING.md doesn't name it but CI does
- https://github.com/emfcamp/Website/issues/1752 — the issue thread;
  its one-line diagnosis ("type == all applied as a filter") pointed
  straight at the view
- https://github.com/emfcamp/Website/tree/main/tests — the repo's own
  test fixtures (conftest.py, `logged_in_client` pattern) my
  regression tests are built on
- https://hub.docker.com/r/postgis/postgis — the test DB needs
  `CREATE EXTENSION postgis`; plain postgres wouldn't have worked
