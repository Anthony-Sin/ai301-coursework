# Evidence guide: where proof lives in a reproduction package

This is the rubric's map. For every proof family a check names, it
says WHERE to look — in an eval bundle and in a live package — and WHAT
GOOD LOOKS LIKE as a condition a second grader could check the same way.

A bundle's parts: the issue context (title, body, thread highlights),
the repo-facts block (bug-report asks, contribution and AI policy), the
candidate claim comment, and the candidate repro report. Live, the
same parts are: the GitHub issue and its thread, the repo's own docs
(CONTRIBUTING, AI_POLICY, issue templates, README), and the student's
draft comments — read as the stranger on the thread will read them.

## Environment

**Where it lives.** In a bundle: the repro report's environment
record — usually an "Environment:" line or block near the top, but any
named versions/OS in the report count, wherever they sit. Read it
against the issue's stated environment (its version/OS lines) and the
repo-facts template asks, and against the dimension the issue turns
on: the driver on a driver-specific bug, the shell on a prompt bug,
the build profile on a release-only crash, the browser's language
list on a locale bug. Live: the same record in the student's draft,
checked against the issue body's stated environment and the repo's
docs.

**What good looks like.** The record names the tool or library
version AND the OS/platform, plus every dimension the issue's trigger
depends on. A stranger could say where this attempt ran and how its
setup differed from the reporter's. When the attempt's environment
differs from the issue's — older or newer version, different OS —
good means the report says so in its own words; a deviation left
unmentioned is the failure signal, not a detail to overlook. Absent
record (no versions, no OS) is a flat fail wherever the report puts
its prose confidence.

## Steps

**Where it lives.** In a bundle: the repro report's steps or commands
section, read against the issue's own reproduction steps and its
trigger description (the exact command, expression, or configuration
the issue names). Live: the same, plus the repo's setup docs the
issue points at.

**What good looks like.** A stranger could re-run the whole attempt
from the report alone, starting state to trigger: file contents are
quoted or constructible, commands carry their real flags, and nothing
essential lives somewhere the reader cannot go — a private repo, an
unshared config, a machine "at work". Good also means faithful: the
steps exercise the trigger the issue describes. A run of a different
syntax, a modified expression, or a renamed-away parameter is not a
re-run of this issue however carefully it is logged — and a step list
that skips the issue's named trigger (a dropped `--driver` flag on a
driver-specific bug) fails even when the output looks right.

## Behavior shown

**Where it lives.** In a bundle: the report's artifacts — the quoted
command output, log excerpts, error text, screenshots-described,
prompt captures — each read against the issue's actual/current-behavior
lines and any maintainer trigger note in the thread highlights (an
owner's "the `--replace` flag is also required" narrows what counts as
the bug). Live: the same artifacts in the draft report.

**What good looks like.** The artifact's content IS the issue's
behavior: the same error identity, the same wrong-value shape, the
same failure mode — not merely the same topic. A control run or
comparison (minus-trigger input, a working sibling case) is the
strongest form. For an honest cannot-reproduce, good means the
artifacts at least come from a genuine run of the issue's trigger.
The failure shapes to catch: artifacts showing a DIFFERENT error or
mechanism than the issue's (an argument-validation rejection standing
in for a capacity-overflow panic, a compile error for an unbound name
standing in for a path-expression bug); artifacts showing only that
the program starts, lists, or renders normally; and "expected" lines
stated backwards from what the artifact shows.

## Honesty

**Where it lives.** In a bundle: the report's conclusion and its
expected-vs-actual lines, plus the claim comment's assertions, all
read against the package's own artifacts — the comparison is inside
the package, not against the world. Live: the same, between the draft
report's claims and its quoted outputs.

**What good looks like.** The stated outcome is exactly what a reader
sees in the artifacts: "reproduced" when a shown artifact is the
issue's behavior; "cannot reproduce" as a real result, carrying what
differed and what a triggering setup likely needs; "partial" when only
part of the issue fired. An evidenced cannot-reproduce is a full pass
here — it is often the most useful comment on the thread. The failure
is a gap between claim and proof in either direction of certainty:
"confirmed", "guaranteed", "100%", "conclusively" over absent or
non-matching artifacts; a root cause asserted with no shown evidence;
a repetition claim ("ran it ten times") standing in for one quoted
run; or generalizing the bug to environments never tested.

## Comms

**Where it lives.** In a bundle: the claim comment, read against the
issue body and thread; and the repo-facts block's contribution policy —
including any AI-use rule — read against BOTH comments. Live: the draft
claim comment against the real issue, and the repo's own CONTRIBUTING /
AI_POLICY / issue-template text against the drafts.

**What good looks like.** The claim names something only this issue
has — the disagreeing files, the observed behavior, the version
tested, a thread pointer — and promises investigation and a report
back, never a fix, a date, or a reservation. Boilerplate is the tell:
a comment that could be pasted under any issue unchanged is not a
claim on this one. On conventions, good means the package satisfies
the rules the repo states: where the policy requires AI-assistance
disclosure, a comment says the tool and the extent; where it requires
the contributor's own words, the comments read as specific
first-person writing; where the policy permits AI use without a
disclosure ask, or says nothing, silence is fine. The template's
field asks are judged under Environment and Steps, not here — this
family governs conduct: disclosure, own-words, no over-promising.
