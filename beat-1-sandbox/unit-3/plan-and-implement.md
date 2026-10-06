# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

Anthony-Sin

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-6008036312

I posted the reproduction above — at `f89c06f` the disagreement is
exactly as the issue describes, and `core/config.py` is the tell:
it defines `openrouter_api_key`, `openrouter_base_url`, and
`openrouter_model` right next to `openai_api_key`. So the template is
the side that disagrees, not the README.

My plan is to fix it from the `.env.example` side — the smallest
change that makes the files agree, in the direction README + SETUP +
`config.py` all point:

1. `.env.example`: add `openrouter` to the `LLM_PROVIDER` options
   comment alongside `mock` and `openai`.
2. `.env.example`: add `OPENROUTER_API_KEY=` (marked required when
   `LLM_PROVIDER=openrouter`) plus commented `OPENROUTER_BASE_URL` /
   `OPENROUTER_MODEL` lines naming their `config.py` defaults.
3. Nothing else — no code changes, README and SETUP stay as they are.

To verify, I'll re-run my repro steps on the branch: after
`cp .env.example .env` the key greps out where it didn't before,
`Settings` loads the documented OpenRouter values, and an unchanged
copy still resolves `mock` so the default path is untouched.

One thing I want to flag rather than decide: `settings.llm_provider`
has no reader in the codebase yet — the only provider factory accepts
`mock`/`openai`. If you'd rather the docs match the wired-up
providers instead (README/SETUP updated to drop OpenRouter), say so
and I'll take that direction — but the three sources pointing at
OpenRouter is why I picked this side.

(Drafted with AI assistance; I read, ran, and edited every line
myself.)

---

## Your branch

**Branch**

`fix/73-env-example-openrouter`

**Evidence**

My Unit 2 reproduction steps re-run against the built change. BEFORE
is `main` at `f89c06f` (re-captured at the start of this unit's
build); AFTER is `fix/73-env-example-openrouter` at `eed03cf`.
Ambient `OPENAI_API_KEY`/`LLM_*` shell variables were unset for the
`Settings` loads exactly as in my posted repro, and `.env` was
deleted afterward; the tree is clean.

BEFORE — step 1, `cp .env.example .env` then look for the key the
README names:

```
$ cp .env.example .env
$ grep -c OPENROUTER_API_KEY .env
0
```

BEFORE — step 4, `.env.example` copied unchanged, same loader:

```
$ env -u OPENAI_API_KEY -u OPENAI_API_BASE -u LLM_API_KEY -u LLM_BASE_URL -u LLM_MODEL \
    /home/ANT/unit2-work/.venv/bin/python - <<'EOF'
from core.config import Settings
s = Settings(_env_file='.env')
print('llm_provider      =', repr(s.llm_provider))
print('openai_api_key    =', repr(s.openai_api_key))
print('openrouter_api_key=', repr(s.openrouter_api_key))
EOF
llm_provider      = 'mock'
openai_api_key    = 'sk-your-key-here'
openrouter_api_key= ''
```

AFTER — on the branch, the same four steps:

```
$ cp .env.example .env
$ grep -c OPENROUTER_API_KEY .env
1
```

Step 2 — the README's implied OpenRouter settings load:

```
$ printf 'LLM_PROVIDER=openrouter\nOPENROUTER_API_KEY=sk-or-test-key-0000\n' > .env
$ env -u OPENAI_API_KEY -u OPENAI_API_BASE -u LLM_API_KEY -u LLM_BASE_URL -u LLM_MODEL \
    /home/ANT/unit2-work/.venv/bin/python - <<'EOF'
from core.config import Settings
s = Settings(_env_file='.env')
print('llm_provider      =', repr(s.llm_provider))
print('openrouter_api_key=', repr(s.openrouter_api_key))
print('openrouter_model  =', repr(s.openrouter_model))
EOF
llm_provider      = 'openrouter'
openrouter_api_key= 'sk-or-test-key-0000'
openrouter_model  = 'google/gemma-3-27b-it:free'
```

Step 3 — all three files now name the same provider set:

```
$ grep -n "OPENROUTER\|Options\|LLM_PROVIDER" README.md docs/SETUP.md .env.example
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)
.env.example:17:# Options: "mock" (default, no API key needed), "openai", "openrouter"
.env.example:18:LLM_PROVIDER=mock
.env.example:20:# Required when LLM_PROVIDER=openrouter (see README Quick Start / docs/SETUP.md)
.env.example:21:OPENROUTER_API_KEY=sk-or-your-key-here
.env.example:23:# OPENROUTER_BASE_URL=https://openrouter.ai/api/v1
.env.example:24:# OPENROUTER_MODEL=google/gemma-3-27b-it:free
```

Step 4 — control, unchanged copy still resolves `mock`:

```
$ cp .env.example .env
$ env -u OPENAI_API_KEY -u OPENAI_API_BASE -u LLM_API_KEY -u LLM_BASE_URL -u LLM_MODEL \
    /home/ANT/unit2-work/.venv/bin/python - <<'EOF'
from core.config import Settings
s = Settings(_env_file='.env')
print('llm_provider      =', repr(s.llm_provider))
print('openrouter_api_key=', repr(s.openrouter_api_key))
EOF
llm_provider      = 'mock'
openrouter_api_key= 'sk-or-your-key-here'
```

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run `--limit 3` (components v1, verifying the install):
   **3/3** — `agreement: 3/3 scored items` (pkg-01 reject, pkg-02
   accept, pkg-03 accept, all agreeing).
2. First full run (same components): **20/20** — `agreement: 20/20
   scored items  (bar: 18/20: PASS)`, categories `clear-accept 7/7
   scope-creep 4/4  thread-convention 2/2  unbuildable 3/3
   wrong-cause 4/4`. No disagreement to revise on.
3. Confirming full run with `--save-run
   beat-1-sandbox/unit-3/eval-run.txt` (same components, unchanged):
   **20/20** — `agreement: 20/20 scored items  (bar: 18/20: PASS)`.
   This is the agreement line in the committed `eval-run.txt`.

**Package analysis**

`pkg-04` (source `junegunn/fzf#4260`, "FZF appears to swallow key
presses when used with `less` on Git Bash"). Gold label: `reject`
(category thread-convention). My rubric's verdict: `reject`, on
`comment-engages-thread` — and `diagnosis-follows-evidence` failed it
independently, which is the interesting part.

The candidate plan is a docs-only workaround (man page note, README
examples, FAQ entry documenting `> /dev/tty`). Read alone it looks
bounded, executable, even honest. But the thread highlights carry the
owner doing the work: reproduced on Windows Server 2025, named the
culprit ("`src/tui/light_windows.go` (lines 70-84)"), posted a patched
test binary at commit `8916cbc`, and asked the reporter to test it.
The plan never mentions any of that — it announces docs as if the
owner's direction were never given. `comment-engages-thread` fails on
exactly that: "the plan routes around explicit maintainer direction
without acknowledging it (a docs-only workaround while a patched
binary sits untested)."

The second fail is what the check was built to notice:
`diagnosis-follows-evidence` grades "the proposed change only
suppresses the measured symptom... while the evidenced cause is named
and left in place" — the plan's own diagnosis names the real cause
(fzf's console input loop keeps reading during an `execute` child),
then its scope explicitly rules out touching it ("Not in scope: any
change to fzf's input handling code"). Naming a cause and then
declining to fix it reads, under the check, as a plan that documents
around the bug — and the gold note agrees: "docs-only workaround plan
whose comment never engages the owner's explicit direction."

**Check rationale**

Quoted verbatim from the `rubric.md` uploaded to `tools/plan-check/`:

> | diagnosis-follows-evidence | The plan's stated cause (its diagnosis, summary, or framing line), read against every step of the package's repro evidence — including each control run, boundary test, and expected/actual pair — and against any cause the thread asserts. | The stated cause explains all of the observed evidence: if this cause is real, every repro step's result follows, including the controls — so removing that cause would remove the measured symptom. A cause the thread asserts also has to survive the package's own evidence; the thread's confidence is not evidence. Fails when any repro step or control contradicts the cause (evidence rules the blamed component out), when the plan adopts a thread-named cause the package's data excludes, when it dismisses a contradicting step by naming it a red herring instead of resolving it, or when the proposed change only suppresses the measured symptom (a guard, a catch-all, a retry on the observable) while the evidenced cause is named and left in place. | required |

It reads this way because the wrong-cause family splits into three
shapes that one pass condition has to hold at once. The
adopt-the-thread's-cause shape is the one our class activity built
around (calib-03): a polished plan inherits the thread's confident
key-binding diagnosis while the package's own timing matrix shows the
26-second cost with no pager in the loop at all — so the check's
evidence column names "any cause the thread asserts" and the pass
condition says the thread's confidence is not evidence. The
dismissal shape is pkg-01: the plan doesn't just miss the
contradicting `--debug` control, it names the version difference "a
red herring," so the clause "dismisses a contradicting step by naming
it a red herring instead of resolving it" catches the move of
acknowledging evidence without answering it. And the
suppress-the-symptom shape is what made pkg-04 fail twice: a plan can
state the cause correctly and still leave it in place, which is not
a wrong-cause plan but is the same family — the evidenced defect
stays. I rejected splitting these into separate checks (one for
contradicted-cause, one for symptom-suppression) because they share
one question — does the fix act on the cause the evidence supports —
and two checks asking it would double-count the same failure on
packages like pkg-04.

**Trade-offs**

The check gives up precision on the legitimately-scoped workaround.
A plan that names the evidenced cause, says "the code fix is out of
scope, here is the documented workaround," AND engages the
maintainer's direction — tells the thread why docs is the right call
against the named culprit — would still fail my
`diagnosis-follows-evidence` clause about leaving the cause in
place, while passing `comment-engages-thread`. I accept that: in this
eval set that shape only exists as pkg-04, where the plan both left
the cause unfixed and ignored the direction, so the strict clause
costs nothing measured. But against a real thread where a maintainer
explicitly endorses a docs workaround, the same clause could reject a
plan the maintainer asked for — the defense is that
`comment-engages-thread` would still pass and only this one check
gates it, which is the disagreement a human review of the run should
catch. Nothing else moved when the clause landed: the clause was in
the components for both full runs, and both runs scored 20/20 with
every category at 100% — including all 7 clear-accepts, three of
which (pkg-09, pkg-13, pkg-14) carry explicit scope deferrals that a
looser reading of "unfixed cause" could have caught.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
