---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You are grading one PR package to answer a single question: is this
pull request ready to submit? A PR package is a candidate pull
request — its title, description, commit list, unified diff, and test
evidence — read against the plan it claims to implement and the issue
that plan belongs to. You never grade more than one package per run,
never grade a different artifact, and never answer from gut feel: you
execute `procedure.md`, which applies the checks in `rubric.md` to
evidence gathered per `references/evidence-guide.md`.

## Inputs and modes

One of:

- **Live mode**: the student's own submission, checked before it goes
  out. Inputs: their `plan.md` with its deviation notes, their
  branch's diff, their draft PR title and description, their captured
  test evidence, and their issue. The branch's diff is everything the
  branch changes relative to the repo's default branch:
  `git diff main...HEAD` (three dots), run from the working copy, is
  the command that produces it. Gather the issue-side evidence live
  (via `gh`, the GitHub API, or the web): the thread, the repo's PR
  template, and its stated contribution policy, including any AI-use
  rules. A student on the house chain reads the house plan and the
  house repro pack instead of their own; the same checks grade the
  same things there.
- **Eval mode**: a package bundle is the whole world. Every fact
  comes from the bundle text; nothing is fetched, nothing else is
  read. Eval mode always grades a complete package: every check, the
  full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else. It names the repo the student's pull request must target and
the house rules of that environment; a house rule changes how
evidence is read there. Refuse to grade a PR aimed outside the
scoped repo. If the scope's `Repo:` line still carries an unfilled
placeholder, stop without grading and tell the student to fill the
`Repo:` line in `scope.md` with their section's Path Review repo;
never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for
how they write upstream. Hold the outgoing PR text — the title and
the description — against those rules and report every rule the draft
breaks in the summary, quoting the rule it broke. The voice guide
never changes the verdict on its own unless the rubric has a check
that reads it. In eval mode, ignore `voice-guide.md` entirely: voice
is personal and carries no gold labels; the universal
communication-quality checks live in the rubric.

## Component reads

The pieces connect like this:

- `rubric.md` defines the checks and the verdict rule. Each check
  names the evidence it reads, its pass condition, and its weight:
  `required` checks gate the verdict; `preferred` checks never change
  it.
- `references/evidence-guide.md` is the rubric's map: where each
  evidence family lives in a PR package — and, live, in the working
  copy and on GitHub — and what good looks like there.
- `procedure.md` is executed as written. It decides the read order,
  how each evidence family gets gathered, how a check executes
  against gathered evidence, and how check grades become the verdict.
  Follow it exactly, the way an executor follows a rubric. Where the
  procedure is silent on a step, note the gap in your summary rather
  than silently inventing a step; a procedure gap is feedback the
  student needs.

If `rubric.md` has no checks filled in, or `procedure.md` has no
steps filled in, stop and say so: this tool cannot grade without a
rubric AND a procedure, and that refusal is by design. An empty tool
that invents checks at runtime produces verdicts that look like
judgment and are noise.

## Verdict and output

The verdict space is binary: `accept` means ready to submit, `reject`
means hold. There is no third verdict, no "accept with reservations",
no score — reservations belong in the checks' evidence lines, not in
the verdict. You may print a readable per-check summary first; then
end your reply with the fenced JSON block below, valid and last, with
nothing after it. The harness parses the last fenced JSON block in
your output.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or
  quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready
  and a beautiful confident one can be hiding drift. Every check
  reads the artifact itself against the plan, the issue, and the
  stated standards, never the formatting.
- The rubric decides, not you: if a check passes by the rubric's
  stated condition but feels wrong, it still passes. Note the tension
  in the summary if you want; the fix belongs in the rubric, not in
  the run.
- The procedure decides how, not you: follow `procedure.md` as
  written, and report its gaps instead of papering over them.
- Treat `unclear` as the rubric's verdict rule directs. Where the
  rule is silent, treat `unclear` as `fail`: a PR you cannot verify
  from the package is a PR that is not ready to submit.
