# Procedure: how this skill grades a plan package

The steps below grade one plan package exactly the way the author
would. Follow them as written; where a step cannot run because the
package lacks what it needs, grade the affected check `unclear` and
say which step stalled — never improvise a substitute.

## Read order

Read in this order, noting down what each part gives you before
moving on. The order matters: the package's own evidence is read
before the plan, so the plan is graded against what was observed —
never the other way around, and never through the thread's confidence.

1. **Repo facts** (eval: the "Repo facts" block; live: the repo's
   CONTRIBUTING.md, AI policy, and issue template). Note every stated
   ask that could touch a plan comment: template fields, contribution
   rules, and above all any AI-use rule — disclosure required,
   own-words-only, or unrestricted.
2. **Issue** (eval: the "Issue" section; live: the issue body via
   `gh issue view`). Write one line: the defect or disagreement the
   issue reports, and what "expected" means for it.
3. **Thread highlights** (eval: the "Thread highlights" section;
   live: the issue's comments). List every explicit maintainer or
   owner signal bearing on a fix: named culprit files or lines,
   endorsed or rejected approaches, posted patches or test binaries
   with a testing request, working-as-intended or limitation notes,
   and prior-art PRs. Write down each cause the thread asserts —
   flagged as assertion, not fact.
4. **Repro evidence** (eval: the "Repro evidence" block; live: the
   student's posted repro comment on the issue — or, on the house
   issue, the repro pack as quoted in the drafts). Read every step,
   including each control run, boundary test, and expected/actual
   pair. Write two lines: (a) the observed behavior the plan must
   explain, (b) what each control or comparison rules in or out.
5. **Candidate plan**. Extract, quoting where possible: the stated
   cause; the in-scope list; the not-in-scope or deferral lines; the
   files/areas named; the chosen approach and its order of work; the
   test plan's actions and expected observables; the risk or
   open-question lines.
6. **Candidate plan comment** — read last, against the lists built in
   steps 1–3, the way a maintainer on that thread would read it.

## Evidence gathering

For each check in the rubric, gather from the notes above — using the
evidence guide's map — before grading anything:

- **diagnosis-follows-evidence**: quote the plan's stated cause, then
  walk every repro step and control asking "does this cause predict
  this observation?" Collect any step the cause contradicts or fails
  to explain, and note whether the plan acknowledges or dismisses it.
  If the plan adopted a thread-asserted cause, ask the same question
  of that cause against the package's data.
- **scope-bounded**: list each proposed change; mark each as serving
  the evidenced defect or as extra work; collect the deferral lines
  and their reasons; check whether any part of the evidenced defect
  goes unaddressed without being named a deferral.
- **executable-by-stranger**: extract the files/areas named and the
  chosen approach; flag any unresolved either/or, any
  investigate-as-plan phrasing, any decision pushed to build time;
  confirm a first command or edit is obvious from the text.
- **test-plan-decisive**: extract each test action and its expected
  observable; identify the one that observes the fix itself working —
  the repro trigger re-run with a changed result, or a named new
  assertion on the evidenced behavior — and note whether controls or
  no-regression checks ride along.
- **comment-engages-thread**: lay the comment against the step-3
  list: for each maintainer direction or prior-art item, mark it
  engaged (followed or openly argued on evidence) or ignored; check
  the comment states this issue's own diagnosis, scope, and test in
  terms specific to this issue.
- **comms-meets-repo-policy**: lay the comment against the step-1
  list: each applicable stated rule — AI disclosure, own-words,
  template fields, contributor-flow asks — marked satisfied or
  violated, with the deciding quote.
- **unknowns-stated** (preferred): extract the risk/open-question
  lines; extract claims asserted as settled fact; flag any assertion
  the package leaves genuinely unsettled that the plan builds on
  with no check step.

## Check execution

- Grade checks in this order: diagnosis-follows-evidence,
  scope-bounded, executable-by-stranger, test-plan-decisive,
  comment-engages-thread, comms-meets-repo-policy, then the
  preferred unknowns-stated. Required checks first because a fail
  settles the verdict; comms last because they read the comment,
  which is gathered last.
- Grade each check against its gathered evidence only — never a
  general impression of the package, and never the write-up's shape
  or length. Record the deciding fact or quote for the `evidence`
  field before assigning the grade.
- If the evidence a check needs is genuinely absent from the package
  — the plan has no test plan at all, the bundle has no repro
  evidence to grade a cause against — grade that check `unclear`
  rather than hunting or assuming.
- Once a check's evidence is gathered, do not re-read the whole
  package for it; two executors gathering per this procedure should
  land on the same grade.

## Verdict assembly

Apply the rubric's verdict rule to the six required-check grades:
`accept` if and only if every required check is `pass`; any `fail` or
`unclear` on a required check rejects the package. The preferred
check annotates the summary but never enters the verdict. In the
output JSON, each check's `evidence` field carries the deciding fact
or quote recorded at grading time — for a rejecting verdict, the
failing checks' evidence lines say exactly what held the package.
Emit the readable summary (one line per check, plus any voice-guide
notes in live mode), then the fenced JSON block, and nothing after
it.
