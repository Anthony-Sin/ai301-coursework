# Procedure: how this tool grades a PR package

The steps below grade one PR package exactly the way the author
would. Follow them as written; where a step cannot run because the
package lacks what it needs, grade the affected check `unclear` and
say which step stalled — never improvise a substitute.

## Read order

Read in this order, noting down what each part gives you before
moving on. The order matters: the plan is read before the diff, so
the diff is measured against what was promised — never the other way
around, and never through the description's confidence.

1. **Repo facts** (eval: the "Repo facts" block; live: the repo's
   `.github/PULL_REQUEST_TEMPLATE.md`, CONTRIBUTING.md, and AI
   policy). List every stated ask that could touch a PR: required
   template sections, required fields (`closes #xxxx`), stated
   changelog/whatsnew/doc entries, contributor-flow asks, and any
   AI-use rule — disclosure required, own-words-only, or
   unrestricted.
2. **Issue** (eval: the "Issue" section; live: the issue body via
   `gh issue view`). Write one line: the defect or request, and what
   "expected" means for it.
3. **Thread highlights** (eval: the "Thread highlights" section;
   live: the issue's comments). List every explicit maintainer or
   owner signal bearing on the fix: posted patches, endorsed or
   rejected approaches, named culprits, testing requests.
4. **Plan context** (eval: the "Plan context" block; live: the
   student's `plan.md`, deviation notes included). Read the repro
   evidence first, then extract from the plan: the stated cause, the
   scope boundary, the files named, each promised deliverable, the
   not-in-scope and deferral lines, every recorded deviation note,
   and the test plan's expected observables. Write the deliverables
   as a checklist — the diff will be walked against it.
5. **Candidate PR** — read last, against the lists built in steps
   1–4. From the title and description, itemize every claim made
   about the change. From the diff, list every changed file and walk
   every hunk. From the test evidence, itemize every observable
   actually shown. From the commits, note the messages.

## Evidence gathering

For each check in the rubric, gather from the notes above — using the
evidence guide's map — before grading anything:

- **diff-matches-plan**: walk the diff file list against the plan's
  scope, named files, and deviation notes — mark each changed file
  and each functional hunk as inside the plan, covered by a
  deviation note, or outside both. Then walk the step-4 deliverables
  checklist against the diff: each marked present, deferred-with-
  disclosure (plan note or description), or missing silently.
- **description-matches-diff**: take each claim itemized from the
  title and description; mark each confirmed by the diff or
  contradicted by it. Fidelity claims ("exactly as planned", "no
  changes beyond") are checked against the step-5 diff walk, not
  taken at face value.
- **test-evidence-decisive**: for each observable in the plan's test
  plan, mark it shown (before/after output, a named new test
  asserting it) or absent; note whether the evidence exercises the
  changed path or only an unchanged control; check the step-1 list
  for repo checks the stated asks require, and whether each was run.
- **diff-reviewable**: scan each hunk for debris — debug prints or
  logging left in, commented-out code or abandoned attempts, dead
  code kept compiling, formatting or whitespace churn unrelated to
  the fix, unrelated hunks folded in. Note the commit messages for
  unfinished-work signals.
- **repo-standards-met**: lay the description's sections and the
  diff against the step-1 list: each applicable stated ask marked
  satisfied (with where) or violated (with what is missing). For a
  disclosure-required AI policy, look for the disclosure line in the
  description itself; the package is treated as AI-assisted work.
- **thread-direction-engaged** (preferred): lay the step-3 signals
  against the approach and description: each marked engaged
  (followed or openly argued on evidence) or ignored.

## Check execution

- Grade checks in this order: diff-matches-plan,
  description-matches-diff, test-evidence-decisive, diff-reviewable,
  repo-standards-met, then the preferred thread-direction-engaged.
  Required checks first because a fail settles the verdict; comms
  last because they read the description, which is gathered last.
- Grade each check against its gathered evidence only — never a
  general impression of the package, and never the write-up's shape
  or length. Record the deciding fact or quote for the `evidence`
  field before assigning the grade.
- If the evidence a check needs is genuinely absent from the package
  — no diff at all, no test-evidence section, no description —
  grade that check `unclear` rather than hunting or assuming.
- Once a check's evidence is gathered, do not re-read the whole
  package for it; two executors gathering per this procedure should
  land on the same grade.

## Verdict assembly

Apply the rubric's verdict rule to the five required-check grades:
`accept` if and only if every required check is `pass`; any `fail`
or `unclear` on a required check rejects the package. The preferred
check annotates the summary but never enters the verdict. In the
output JSON, each check's `evidence` field carries the deciding fact
or quote recorded at grading time. For a rejecting verdict, the
deciding line is the evidence of the first failing required check in
rubric order; when several fail, the rest are reported in their own
evidence lines. Emit the readable summary (one line per check, plus
any voice-guide notes in live mode), then the fenced JSON block, and
nothing after it.
