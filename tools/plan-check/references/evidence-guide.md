# Evidence guide: where evidence lives in a plan package

The skill uses this guide as its map: for every kind of evidence a
rubric check names, this file says WHERE to find it in a plan package
and WHAT GOOD LOOKS LIKE when you do. In an eval bundle the package is
the whole world; live, the same families sit on the issue thread, in
the student's posted repro comment, in the repo's docs, and in the
draft plan and comment.

## Diagnosis and grounding

- **Where it lives**: the plan's Diagnosis, Summary, or framing line —
  wherever it states what causes the defect. Read it against the
  repro-evidence block's steps AND its control runs, boundary tests,
  and expected/actual lines (in a bundle, the "Repro evidence"
  section; live, the student's posted repro comment on the issue).
  Also read the thread highlights for any cause a maintainer or
  commenter asserts — the plan may adopt it.
- **What good looks like**: the stated cause, taken as true, predicts
  every observation the package records — including each control,
  since a control that rules a component out makes any plan blaming
  that component a wrong-cause plan. A plan that names the thread's
  confident diagnosis must still survive the package's own data; a
  contradicting step the plan never resolves is a fail, not a
  disagreement of opinions.

## Scope

- **Where it lives**: the plan's Scope section — its in-scope
  statement, its not-in-scope line, its stated deferrals — plus the
  full list of proposed changes and files, read against what the
  issue and repro evidence ask for.
- **What good looks like**: every listed change serves the evidenced
  defect, and whatever part of the defect is left unfixed is named as
  a deferral with a reason. One bounded change can sit beside an
  honest deferral list; a fix inside a redesign, migration, new
  option surface, or "while in the area" repair cannot, no matter how
  correct the core is.

## Executability

- **Where it lives**: the plan's Approach, Changes, Steps, and
  Files/areas sections — whatever tells the builder what to do.
- **What good looks like**: named files or areas, one chosen approach
  (alternatives may be discussed, one is picked), and an order of
  work a stranger could start on without a single question back.
  Decisions pushed to build time — "whichever is easier", "not sure
  which layer", "maybe also check other X" — and investigation posed
  as a plan ("look into", "profile", "poke around") are the failure
  shapes.

## Test plan

- **Where it lives**: the plan's Test plan section, read against the
  repro evidence's steps and artifacts — the trigger command, its
  observed output, the controls.
- **What good looks like**: an observable outcome for the fix itself:
  the repro trigger re-run with its expected changed result (an
  output, an exit code, a timing, a rendered state) or a named new
  test asserting the evidenced behavior. "Run the full suite" may
  ride along but cannot be the whole plan; "should feel fast" and
  "nothing else should break" name no observable at all.

## Honesty

- **Where it lives**: the plan's risk lines, open questions, and
  check-at-build notes, read against every claim it asserts as
  settled fact — including claims about what the code does today.
- **What good looks like**: unknowns the plan hinges on are named as
  unknowns — flagged for review, unmeasured costs admitted, a check
  to run first. Asserting as verified fact something the package
  leaves open, with no check step behind it, is the failure shape;
  a plan with nothing genuinely unsettled owes no risks section.

## Comms

- **Where it lives**: the candidate plan comment, read against the
  thread highlights (or live, the real thread) and the repo-facts
  block's stated asks — bug-report template, contributing guide, and
  any AI-use policy (live: CONTRIBUTING.md, AI_POLICY.md, or their
  equivalents in the repo's docs).
- **What good looks like**: the comment engages explicit maintainer
  direction present in the thread — follows it or argues an
  alternative on the evidence — acknowledges prior-art PRs it would
  otherwise race, satisfies the repo's stated policy including any
  required AI disclosure, and carries specifics only this issue could
  carry. Boilerplate, piggybacking on another's plan, and a route
  around the maintainer's stated direction are the failure shapes.
