# Evidence guide: where evidence lives in a PR package

The tool uses this guide as its map: for every kind of evidence a
rubric check names, this file says WHERE to find it in a PR package
and WHAT GOOD LOOKS LIKE when you do. In an eval bundle the package
is the whole world; live, the same families sit in the student's
`plan.md`, in the branch's diff, in the draft PR text and captured
test output, and on the repo's own pages.

## Plan fidelity (harness category: silent-drift)

- **Where it lives**: the plan-context block's scope statement,
  named files, not-in-scope and deferral lines, and deviation notes
  (live: `plan.md`, its Scope and Deviations sections) — read
  against the candidate PR's diff, file by file and hunk by hunk.
  Read both directions: work the diff does that the plan never
  asked for, and deliverables the plan promised that the diff does
  not contain. The description's fidelity claims read against the
  diff live here too: a description claiming more or less than the
  diff delivers is silent drift, not a comms problem.
- **What good looks like**: every changed file and functional hunk
  maps to a planned change or a recorded deviation note, and every
  planned deliverable appears in the diff or is disclosed as
  deferred — in a plan note or in the description itself. The
  failure shapes: unannounced extras (a new flag, option, or
  setting; a rename or refactor pass; adjacent "cleanup"; help-text
  rewrites), silently missing deliverables, and fidelity language
  ("implements the plan exactly", "no functional changes") that the
  diff contradicts. An honest deferral stated where a reader sees
  it is not drift.

## Test evidence (harness category: not-tested)

- **Where it lives**: the PR's test-evidence section, read against
  the plan's test plan and the reproduction's own steps — the
  trigger command, its observed output, the controls (live: the
  captured test output the student pastes). The repo-facts block's
  stated checks and suite asks bound what "ran the checks" means.
- **What good looks like**: each observable the plan's test plan
  named is shown exercised — the repro trigger re-run before/after
  with the expected changed result (an output, an exit code, a
  timing, a rendered state), or a named new test asserting the
  evidenced behavior — and the repo's own suite or checks run where
  the stated asks require them. The failure shapes: evidence that
  exercises only the unchanged path (a control presented as the
  result), "tests pass", "verified working", or "tested locally"
  with no named observable, the plan's repro never re-run, and a
  stated repo check never shown to have run.

## Diff quality (harness category: unreviewable)

- **Where it lives**: the unified diff itself, hunk by hunk, and the
  commit list.
- **What good looks like**: the fix is visible — a reviewer reads
  the change, its test, and any stated doc entries, and nothing
  else. The debris tells: leftover debug prints or logging,
  commented-out code or abandoned first attempts, dead code kept
  compiling (unused functions, `allow(dead_code)`, unreachable
  blocks), formatting or whitespace churn unrelated to the fix,
  unrelated hunks folded in, and commit messages that read as
  unfinished work ("wip", "fix", "misc cleanups while debugging").

## Standards and comms (harness category: standards-wall)

- **Where it lives**: the repo-facts block's stated PR-template
  asks and contribution policy — required template sections,
  required fields, stated changelog/whatsnew/doc entries, the
  AI-use rules — read against the PR description's sections and
  the diff itself (live: `.github/PULL_REQUEST_TEMPLATE.md`,
  CONTRIBUTING.md, the repo's AI policy page).
- **What good looks like**: every stated ask that applies is
  honored — template sections filled with real content rather than
  left as prompts or skipped, required fields like `closes #xxxx`
  present, stated doc entries actually present in the diff, and
  AI-use disclosure (the tool and the extent of the assistance)
  present where the stated policy requires it; every package is
  treated as AI-assisted work, so a disclosure-required policy
  holds the description to that. The failure shapes: a required
  template visibly ignored, boilerplate under a required heading,
  a stated entry absent from the diff, a required disclosure
  missing. Whether the description's claims match the diff is plan
  fidelity, above — not here.
