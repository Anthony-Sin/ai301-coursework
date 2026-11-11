# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

This file is Assignment 6, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. It has been waiting here since you created the repo in unit 1;
unit 9 is when you write it.

**Only this page is read.** Your `tools/` folders and your installed skill folders are never
opened, so every piece of evidence you want seen has to live inline here: an output excerpt,
a before/after pair, a dated commit reference.

**Write every sentence yourself.** AI may gather diffs, dates and excerpts for you; it does
not draft entries.

**Keep every section header below under its exact name** — Featured Tools, Inventory, The
Arc, and Limitations and What's Next. Feature three or four tools, each in the entry shape
shown below; give every other tool one inventory line.

**Student:** Anthony Sinchi

## Featured Tools

I featured the four tools that made it to the wild and actually did
work there: the scout that picked my issue, the guard that checked
what I posted upstream, the gate that stood in front of my PR, and
the monitor that watches it now. These are also the four that visibly
changed through use — the beat-1 graders (issue-select, repro-check,
plan-check, pr-precheck) moved less and live in the inventory.

**issue-scout**

**What it is, and the judgment hole I wrote:** A wild-GitHub issue
scout: it runs my `gh search issues` queries, ranks the results with
my filters, and grades the top five against my rubric. The judgment
holes are mine end to end — the rubric (carried forward from unit 1,
then patched), the fit profile, and `search-strategy.md` (three
queries each traced to a profile sentence; ranking rules: drop
assigned, drop 60-day-stale, drop No-AI labels, order fewest comments
first).

**How it evolved, dated:** 2026-09-22 the rubric was born for the
sandbox (20/20 eval, committed in unit 1). 2026-11-10 I installed the
scout over it (staff SKILL.md, real-repos scope, my strategy) and ran
the first real scan: 300 raw hits → 266 after dedupe and drops. Same
day I applied the unit-6 patch: my unit-1 `scope-fits-newcomer` check
became `scope-feasible` — scope stopped rejecting open edges and
became a difficulty note instead — and I graded my three site picks
with it.

**Evidence:** The patch earned itself on real picks the same day —
my scout's direct grading of the three issues I shortlisted on the
Issue Selection site:

```text
1. accept — emfcamp/Website#1752 — difficulty: straightforward
2. reject — render-engine/render-engine#1310
   contribution-policy: issue carries a `No-AI` label; maintainer
   stated in-thread he prefers no LLM help on docs issues
3. reject — piscinajs/piscina#1029
   scope-feasible: described bug already fixed by merged PR #1030
```

Both rejects are things I would have missed reading titles alone: a
label that forbids my honest workflow, and an issue whose bug no
longer exists. I claimed the accept; it's the contribution in
Assignment 5 (PR emfcamp/Website#2394).

**voice-guard**

**What it is, and the judgment hole I wrote:** A hook that runs my
voice guide against anything I'm about to post upstream. The judgment
hole is the guide itself at
`~/.claude/voice-guard/voice-guide.md` — my rules for sounding human
and being honest, including the Upstream section I wrote in unit 6
(claims, questions, pings; each a `#### Rule:` with a wrong/right
pair).

**How it evolved, dated:** 2026-09-29 the guide started inside
repro-check (unit 2). 2026-11-10 it was promoted to one canonical
home and symlinked back into the three check skills, and I wrote the
Upstream section: the rule that earned itself first was "a claim says
what you'll do and when you'll report back" — my first claim draft
for emfcamp#1752 had no check-in date, and the guard (well, the rule,
checked by hand against the draft) sent it back before it posted.

**Evidence:** Before/after on my claim draft, 2026-11-10:

```text
before: "...then look at how the view handles the filter value."
after:  "...I'll report back here within about a week, either with a
        PR or with what I found. (Doing this as part of a university
        open-source course; I use AI assistance in my workflow and
        review everything myself before posting.)"
```

The posted comment carries the after:
https://github.com/emfcamp/Website/issues/1752#issuecomment-6787597383

**ship-gate**

**What it is, and the judgment hole I wrote:** A hook that runs the
target repo's own checks plus my pr-precheck before a PR may open.
The judgment hole is `ship-manifest.md`: which checks the project
actually demands (read from `.github/workflows/test.yml`, not
CONTRIBUTING.md, which is one page pointing at IRC), and — the real
judgment — what legitimately belongs in the excluded table and why.

**How it evolved, dated:** 2026-11-10 installed into my emfcamp/Website
clone (manifest created, working files git-excluded, hook in
settings.json). Same day the interesting thing happened: the full
pytest suite showed a failure that was real but not mine.

**Evidence:** `tests/volunteer/test_role.py::test_grouped_by_team`
fails on an unmodified upstream `main` checkout — I stashed my two
changed files and re-ran it to prove it before writing the manifest
row:

```text
## Excluded, with a dated reason
| full pytest suite | ... pytest tests -q | 2026-11-10 |
| tests/volunteer/test_role.py::test_grouped_by_team fails
| identically on unmodified upstream main (seeded-data assertion);
| unrelated to messages sorting |
```

The alternative was either silently ignoring a red suite or shipping
a fake "all green"; the excluded table is the honest middle — visible
to my pr-precheck, dated, reasoned.

**pr-monitor**

**What it is, and the judgment hole I wrote:** A script that reads my
open PR (checks, reviews, comments, quiet days) and drafts a next move
I decide on. The judgment hole is `playbook.md`: response rules,
staleness thresholds, nudge etiquette, walk-away criteria — written
for emfcamp/Website specifically.

**How it evolved, dated:** 2026-11-10 installed and playbook written.
The threshold isn't a vibe: I sampled the repo's merged PRs and found
outside-contributor PRs merging same/next-day during July's event
crunch but a quiet repo off-season, so my nudge threshold is 14 quiet
days (halved May–Aug). 2026-11-11 first `--state` run against the real
PR.

**Evidence:**

```text
# PR-monitor run report (2026-11-11 00:14)
- PR: https://github.com/emfcamp/Website/pull/2394
- checks: no checks reported
- mergeable: MERGEABLE (merge state BLOCKED)
- review decision: none yet
- state: QUIET: the thread is quiet: under a day since the last
  activity by anyone but you
- playbook: all four sections filled in, ready for a full run
```

It reads my PR correctly and it knows my playbook is complete. The
real test is still ahead — whether its draft is worth posting when a
review actually lands.

## Inventory

- issue-select: the unit-1 sandbox grader (rubric + scope + evidence
  guide) — retired into the scout; it still grades eval bundles 20/20.
- repro-check: reproduction-package grader; swapped to the wild scope
  in unit 6 — graded my claim draft and repro report for #1752
  (accept; flagged the missing "how do you get an admin login" step).
- plan-check: plan-package grader; wild scope — graded my plan for
  #1752 and its objection ("is view-only enough?") is why the fix is
  two-sided.
- pr-precheck: PR-package grader; wild scope installed by the
  ship-gate install — runs inside the gate rather than standalone now.
- CLAUDE.local.md (repo memory): the distilled emfcamp subsystem map
  (view, template, sort fn, blueprint prefix, fixture login) — saved
  a second orientation pass when I returned to build.

## The Arc

**Beat 1**
Date: late September 2026 (unit 2, commit 2026-09-29)
Friction: my first claim/repro drafts read like a press release —
"I am excited to announce" voice, no dates, no mechanism
Change: wrote the voice guide's general rules (sound like a person
doing work; one idea per sentence; never claim results I haven't seen)
Result: my sandbox claim and repro comments on #73 posted in the new
voice, and the guide became the thing every later tool defers to

**Beat 2**
Date: 2026-11-10 (unit 5)
Friction: my unit-1 scope check rejected issues for the open edges
that real wild issues always carry — a strict sandbox rule
Change: applied the staff patch — `scope-fits-newcomer` out,
`scope-feasible` in, plus the difficulty-note section; logged the
replacement in scan-notes.md
Result: the scout's next run graded my three site picks and caught a
`No-AI` label and an already-merged fix — two rejects I'd have missed
by title

**Beat 3**
Date: 2026-11-10 (unit 6)
Friction: the voice guide existed in three drifting copies across
check skills, and had nothing to say about claims/questions/pings —
the three things I'd actually post upstream
Change: promoted it to `~/.claude/voice-guard/voice-guide.md`,
symlinked into the skill folders, wrote the Upstream section
Result: the guard's claim rule sent my first claim draft back for a
missing check-in date before it posted — the posted comment carries it

**Beat 4**
Date: 2026-11-10 (unit 7)
Friction: the full test suite was red on a failure that wasn't mine,
and "the suite is green" and "ignore the suite" were both dishonest
Change: verified the failure reproduces on clean main, then wrote it
into the ship-manifest's excluded table with a dated reason and
scoped the gate's pytest row to the area my PR touches
Result: the gate ran green on signal that matters and the skipped row
is on the record instead of hidden — the PR opened with honest checks

**Beat 5**
Date: 2026-11-10 (unit 8)
Friction: "when is a quiet PR too quiet" was a number I'd have pulled
from air
Change: sampled emfcamp/Website's merged PRs (same/next-day in event
crunch, quiet repo off-season) and wrote 14 days into the playbook
Result: `monitor.py --state` reads my real PR and its QUIET call is
now backed by data I can defend to a maintainer

## Limitations and What's Next

The toolkit's honest state: every piece did real work on one
contribution, exactly once. Nothing here has survived a second issue,
a hostile maintainer, or a review cycle yet — the monitor has never
drafted a reply, the gate has never stopped a PR it should have, and
the scout's ranking still rewards quiet threads over good fit. The
tools grade my judgment; they can't yet tell me my judgment was right.

What's next: feed the scout's "why it rejected" list back into the
strategy (penalize machine-filed issues), run the monitor on a real
review when one lands and see if the draft survives my own voice
guide, and promote CLAUDE.local.md's pattern (subsystem map +
env workarounds) into a template so the second repo costs less than
the first.

**Tool limits.**

issue-scout: its ranking optimizes for silence (fewest comments),
which surfaced bulk-filed analyzer issues that pass every check but
make poor claims; it can't read "is this repo's issue tracker real"
voice-guard: it only sees drafts I route through it — anything typed
straight into a GitHub text box bypasses it unless I remember the
manual check; and it judges style, not whether my content is right
ship-gate: it can't see that a check it skipped is already red
upstream — the excluded table is only as honest as the verification I
do by hand before writing the row
pr-monitor: untested against an actual review — its draft quality is
unproven, and its staleness counts days, not context (a maintainer's
"looks fine, next release" reads the same as silence)
