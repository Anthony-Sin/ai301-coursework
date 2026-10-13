# Rubric: is this pull request ready to submit?

A package is a candidate PR — title, description, commits, diff, test
evidence — read against the plan it claims to implement and the issue
that plan belongs to. Every check below judges an OUTCOME a reviewer
could verify from the package — never the write-up's shape, length,
headings, or polish. `references/evidence-guide.md` says where each
named evidence lives, in an eval bundle and live.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diff-matches-plan | The diff's changed files and hunks, read against the plan's scope statement, its named files, its not-in-scope and deferral lines, and its recorded deviation notes (bundle: the plan-context block; live: `plan.md`). | The diff lands inside the plan's stated scope or a recorded deviation note, and every deliverable the plan promised is present in the diff — unless it is explicitly deferred, and the deferral is recorded in the plan or stated in the PR description. An honestly disclosed shortfall passes; silent drift fails in both directions: more than the plan (unplanned options, settings, flags, renames, refactors, help-text rewrites, "while in the area" work) and less than the plan (a promised deliverable absent with no deferral recorded anywhere). | required |
| description-matches-diff | The PR title and description's claims about what changed, read against the actual diff contents and the plan. | Every claim the description makes about the change is true of the diff: disclosed deferrals and plainly named extras count as honest claims. Fails when the description asserts fidelity the diff contradicts — "implements the plan exactly", "no changes beyond the plan", "no functional changes outside X" over a drifting diff — or claims a deliverable the diff does not contain (docs updated, tests added, a file changed that is not in the diff). | required |
| test-evidence-decisive | The PR's test-evidence section, read against the plan's test plan and the reproduction's own steps, plus the repo-facts block's stated checks or suite where the stated asks require them. | Each observable the plan's test plan named is shown exercised: the repro trigger re-run with its expected changed result (before/after output, exit code, timing, rendered state), or a named new test asserting the evidenced behavior; and the repo's own checks or suite were run where the repo's stated asks require them. Fails when the evidence exercises only the unchanged path (a control run presented as the result), when "tests pass", "works on my machine", or "verified" stands in for a named observable, when the plan's repro is never re-run, or when a required repo check is never shown to have run. | required |
| diff-reviewable | The unified diff read hunk by hunk, plus the commit list. | The change is visible and nothing unrelated rides along: a reviewer sees the fix, its test, and any stated doc entries. Fails on debris — leftover debug prints or logging, commented-out code or abandoned first attempts, dead code kept compiling (unused functions, `allow(dead_code)`, unreachable blocks), formatting or whitespace churn unrelated to the fix, unrelated hunks folded in — or a commit trail that reads as unfinished work ("wip", "misc", "fmt + cleanup"). | required |
| repo-standards-met | The repo-facts block's stated PR-template asks and contribution policy — above all its AI-use rules — plus any stated doc-entry asks (changelog, whatsnew), read against the PR description's sections and the diff (live: `.github/PULL_REQUEST_TEMPLATE.md`, CONTRIBUTING.md, the repo's AI policy). | Every stated ask that applies is honored: required template sections filled with real content (not left as prompts, not skipped), required fields present (`closes #xxxx`, issue references), stated changelog/whatsnew entries present in the diff itself, and AI use disclosed with the tool and the extent of the assistance where the stated policy requires disclosure — these packages are treated as AI-assisted work, so a disclosure-required policy fails on a description carrying no disclosure. A repo stating no applicable asks, or a policy permitting AI with no disclosure requirement, passes on that front. | required |
| thread-direction-engaged | The thread highlights' explicit maintainer or owner signals bearing on the fix — a posted patch, an endorsed or rejected approach, a named culprit — read against the PR's chosen approach and description. | When the thread carries explicit maintainer direction, the PR follows it or openly argues an alternative on the evidence, and the description shows that engagement; when the thread carries none, the check passes on a description that states this change's own scope and evidence in terms specific to this issue. Fails when the PR routes around explicit maintainer direction without acknowledging it. | preferred |

## Verdict rule

Accept if and only if every required check grades `pass`. A required
check graded `fail` or `unclear` rejects the package: `unclear`
counts as `fail`, because a PR the grader cannot verify from the
package is a PR that is not ready to submit. The preferred check
never enters the verdict — it annotates an accepted package's
strength or a rejected one's salvageable parts, nothing more.
