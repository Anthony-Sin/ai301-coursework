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

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/167

**Branch**

`fix/73-env-example-openrouter`

## Eval iterations

**Run history**

Two runs, in order: a `--limit 3` smoke run that agreed 3/3 on the
packages it graded (a partial run, so no bar verdict), then one full
20-package run that agreed **20/20 scored items (bar: 18/20: PASS)**,
with the category floor met in all five categories (`clear-accept
7/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2,
unreviewable 3/3`). The committed `eval-run.txt` is that second run;
its agreement line reads `agreement: 20/20 scored items`.

**Package analysis**

pkg-20 (category `standards-wall`, source `ghostty-org/ghostty#13604`).
My rubric decided `reject`; the gold label is `reject`. The package is
a strong fix — gold's own note calls it an "excellent bounded fix
implementing the maintainer-authored diagnosis with decisive
mode-2031 evidence" — so the hold comes from exactly one place: the
repo-facts block states the contribution policy is "strict AI rules.
All AI usage in any form must be disclosed, stating the tool used and
the extent of the assistance," and the PR description carries no
disclosure line anywhere. My rubric's `repo-standards-met` check
reads that stated policy against the description, and because the
check is written to treat "these packages [...] as AI-assisted work,
so a disclosure-required policy fails on a description carrying no
disclosure," the missing disclosure is a `fail` on a `required`
check. The verdict rule — "a required check graded `fail` or
`unclear` rejects the package" — does the rest. The run's per-check
evidence named `repo-standards-met` as the failing check, which is
why I know the tool held it for the stated policy and not for
anything in the diff.

**Check rationale**

From `rubric.md`, the `diff-matches-plan` pass condition, verbatim:

"The diff lands inside the plan's stated scope or a recorded
deviation note, and every deliverable the plan promised is present
in the diff — unless it is explicitly deferred, and the deferral is
recorded in the plan or stated in the PR description. An honestly
disclosed shortfall passes; silent drift fails in both directions:
more than the plan (unplanned options, settings, flags, renames,
refactors, help-text rewrites, "while in the area" work) and less
than the plan (a promised deliverable absent with no deferral
recorded anywhere)."

It reads that way because drift runs in both directions and the eval
set tests both: pkg-03, pkg-06, and pkg-09 add work the plan scoped
out (a new config option, a renaming pass, a `--time-format` flag),
while pkg-17 delivers only half the plan — "the plan promises a dev
warning AND a docs update; the diff contains only the warning."
A check that only scanned for extra files would pass pkg-17, and a
check that equated "less than everything" with "hold" would reject
the honest shortfalls the set accepts (pkg-13, pkg-16, where the
deferral is recorded in the plan and restated in the description).
So the condition names both directions of silence and carves out the
disclosed deferral: the sin is the silence, not the shortfall.

**Trade-offs**

What `test-evidence-decisive` gives up: it grades the evidence shown
in the package, not whether the run behind it actually happened.
A package carrying fabricated before/after output would pass it,
because in eval mode "the bundle text is your only evidence." I
accept that gap deliberately: a text grader cannot verify a run
occurred, and tightening the check to demand stronger proof would
punish exactly the terse-but-real evidence the clear-accepts carry
(pkg-11, pkg-19) without catching a liar any better. The honest
version of the limit is stated rather than hidden, which is what the
check's own pass condition asks of PRs. Nothing else changed on the
way to the committed run, and here is how I know: only two runs ever
happened (the 3-package smoke and the full run), no check was
revised or loosened between them, and the full run's table shows a
match in every category — a blind-spotted rubric would have left a
`NO` in the `agree` column somewhere.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
