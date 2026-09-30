# Rubric: is this reproduction package ready to post?

A package is a claim comment plus a repro report, read against the
issue they belong to. Every check below judges an OUTCOME a stranger
on the thread could verify — never the write-up's shape, length, or
formatting. `references/evidence-guide.md` says where each named
evidence lives, in an eval bundle and live.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| environment-recorded | The repro report's environment record, read against the environment the issue targets (versions, OS, and the issue's load-bearing dimension: driver, shell, browser, build profile, config file contents) and the repo-facts bug-report asks. | An environment record exists that names the tool/library version and the OS/platform, plus whatever dimension the issue's trigger depends on. A stranger could say where this attempt ran. No record at all, or a record missing a dimension the issue's trigger depends on, fails. Whether a deviation undermines the result is judged under evidence-bears-on-issue, not here. | required |
| steps-rerunnable | The repro report's steps/commands, read against the issue's own reproduction steps and trigger description. | A stranger could re-run the attempt from the report alone: the starting state is given or constructible (file contents quoted, commands shown), the exact commands with their flags are present, and the run reaches the trigger the issue names — the same input syntax, expression, or configuration the issue describes, not a neighbor of it. Missing steps, steps that depend on private or unshared materials (a company repo, an internal config), or steps that swap the trigger for something adjacent, fail. | required |
| evidence-bears-on-issue | The report's artifacts — the quoted command outputs, logs, error text, observed states — each read against the behavior the issue describes (its actual/current-behavior lines and any maintainer trigger note in the thread). | The artifacts come from exercising the issue's question on a target the issue's claim covers: they either show the issue's described behavior (same symptom, error identity, or failure mode), or — on an honest cannot-reproduce — show a genuine run of the issue's trigger whose result the report states plainly. Fails when the artifacts show a different error or mechanism than the issue's and are presented as it, when they show only that the program starts or runs normally, when nothing quoted bears on the issue's behavior at all, or when the run silently targeted something the issue's claim does not cover — a version far outside the issue's stated or confirmed range, exercised with the difference left unexplained, so the artifact cannot speak to the reported bug. | required |
| outcome-honest | The report's conclusion, expected-vs-actual lines, and the claim comment's assertions, read against what the package's own artifacts actually show. | The stated outcome matches the shown evidence: "reproduced" only when an artifact shows the issue's behavior; an evidenced cannot-reproduce or partial result stated plainly passes; claimed certainty never outruns what is quoted ("ten identical runs" and "100% reproducible" count only if at least one run's output is actually shown). Asserting confirmation, a root cause, or a crash the artifacts do not show fails. | required |
| claim-specific-honest | The claim comment, read against the issue body and thread and against the report it points at. | The comment names at least one thing specific to THIS issue (the behavior observed, the version tested, a pointer from the thread) and states an honest intent — investigate, reproduce, report back — that the accompanying report does not contradict. Fails on interchangeable assign-me or +1 boilerplate that could sit under any issue, on a promised fix or a promised date, on reserving the issue, or on claiming results the report does not contain. | required |
| conventions-respected | The repo-facts block's stated bug-report asks and contribution policy — especially any AI-use rule — read against the package's two comments. | Every stated rule that applies to the comments is honored. These packages are treated as AI-assisted work: a policy requiring disclosure of AI assistance fails unless a comment actually discloses the tool and extent of the help; a policy requiring the contributor's own words fails only if a comment reads as generic boilerplate rather than specific first-person writing; a policy that permits AI without a disclosure ask, or no stated policy at all, passes on that front. The template's asks are enforced by the environment and steps checks; this check governs conduct, not fields. | required |
| control-or-isolation | Any control run, minus-trigger comparison, or boundary test in the repro report. | Present when the report includes at least one comparison that isolates the trigger (a run without the trigger input, an adjacent configuration, a second shape of the same bug). Absence never fails the package; presence only sharpens the summary. | preferred |
| next-step-named | The claim comment's or report's forward-looking lines, read against the issue thread's pointers. | Present when the package names a concrete next investigative step tied to this issue (a code area, a maintainer's pointer, an upstream thread, a test to write). Absence never fails the package. | preferred |

## Verdict rule

Accept if and only if every required check grades `pass`. A required
check graded `fail` or `unclear` rejects the package: proof the grader
cannot verify is proof that is not ready to post. Preferred checks
never change the verdict — they only annotate an accepted package's
strength or a rejected one's salvageable parts. On a claim-only draft,
the checks that need the repro report are not applicable and stay out
of the verdict entirely; the verdict then answers only whether the
claim comment is ready to post.
