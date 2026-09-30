# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

Anthony-Sin

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5903132438

Hi, I'd like to work on this docs disagreement as my first contribution here.

Reading the three files against each other: `README.md` (Quick Start) and `docs/SETUP.md` both tell a newcomer to add `OPENROUTER_API_KEY` to `.env` — SETUP even calls it required for AI features. But the `.env.example` the docs tell you to copy has no `OPENROUTER_API_KEY` line at all, and its `LLM_PROVIDER` comment offers only `mock` and `openai`. `core/config.py` defines `openrouter_api_key`, `openrouter_base_url`, and `openrouter_model` right next to `openai_api_key`, so the code knows about OpenRouter; the template doesn't.

My next step is reproducing the disagreement end to end: `cp .env.example .env` per the docs, then load `core/config.py`'s `Settings` under each documented path — one following the README's OpenRouter instruction, one following `.env.example` as shipped — and capture what each leaves in the settings object. I'll post the full report here, with environment and outputs, before suggesting which side should change.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5903181246

## Reproduction report: `README.md` vs `.env.example` API-key disagreement (#73)

**Result: reproduced.** `README.md` tells a newcomer to add `OPENROUTER_API_KEY` to `.env`, while the `.env.example` you actually copy doesn't list that variable and offers only `mock`/`openai` for `LLM_PROVIDER`. `core/config.py` defines both keys. Everything below is from my own run.

### Environment

- OS: Arch Linux (kernel 7.2.4-arch1-2, x86_64)
- Python: 3.14.7, in a venv with `pydantic` 2.13.5 and `pydantic-settings` 2.15.0 (the two packages `core/config.py` imports)
- Repo: my fork `Anthony-Sin/pathreview-ai301-fa26-s1`, `main` at `f89c06fc3ff292df2a04a39ac51319d32a76b779` (`f89c06f`), clean tree before and after
- Limits: `docker compose` is not available on this machine (Docker CLI is, the compose plugin isn't), so I did not start the backing services. This bug doesn't need them — it lives in the setup docs and the config layer, which is what I exercised. I also unset my shell's ambient `OPENAI_API_KEY`/`LLM_*` variables for these runs so the outputs show only what `.env` provides.

### Steps

**1. What each doc says, verbatim:**

```
$ grep -n "OPENROUTER" README.md docs/SETUP.md
README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)

$ grep -n "Options\|LLM_PROVIDER\|API_KEY" .env.example
17:# Options: "mock" (default, no API key needed), "openai"
18:LLM_PROVIDER=mock
19:OPENAI_API_KEY=sk-your-key-here
```

**2. Follow the documented copy step, then look for the key the README names:**

```
$ cp .env.example .env
$ grep -c OPENROUTER_API_KEY .env
0
```

The file the docs tell you to copy has no `OPENROUTER_API_KEY` line to fill in, and its provider comment offers only `mock` and `openai`.

**3. Path A — a newcomer who follows the README's instruction.** I rewrote `.env` with the README's implied settings (`printf` the OpenRouter lines in place of the `mock`/`openai` block), then loaded `Settings` exactly as `core/config.py` defines it, from the repo root in the venv:

```
$ printf 'LLM_PROVIDER=openrouter\nOPENROUTER_API_KEY=sk-or-test-key-0000\n' > .env
$ env -u OPENAI_API_KEY -u OPENAI_API_BASE -u LLM_API_KEY -u LLM_BASE_URL -u LLM_MODEL \
    python - <<'EOF'
from core.config import Settings
s = Settings(_env_file='.env')
print('llm_provider      =', repr(s.llm_provider))
print('openai_api_key    =', repr(s.openai_api_key))
print('openrouter_api_key=', repr(s.openrouter_api_key))
print('openrouter_model  =', repr(s.openrouter_model))
EOF

llm_provider      = 'openrouter'
openai_api_key    = ''
openrouter_api_key= 'sk-or-test-key-0000'
openrouter_model  = 'google/gemma-3-27b-it:free'
```

`Settings` accepts `openrouter` silently — `llm_provider` is a free string field, so nothing warns the newcomer at config time. To check whether the codebase supports that provider anywhere, I probed the only provider factory that exists, `get_embedding_provider` in `ingestion/embeddings/provider.py` — a probe I ran by hand in the same venv (`python` REPL from the repo root); see step 5, nothing in the app calls it today:

```
>>> from ingestion.embeddings.provider import get_embedding_provider
>>> get_embedding_provider('openrouter')
ValueError: Unknown embedding provider: openrouter. Supported: 'mock', 'openai'
```

**4. Path B — a newcomer who follows `.env.example` as shipped.** `.env` copied unchanged (`cp .env.example .env`), same loader with the factory call added:

```
$ env -u OPENAI_API_KEY -u OPENAI_API_BASE -u LLM_API_KEY -u LLM_BASE_URL -u LLM_MODEL \
    python - <<'EOF'
from core.config import Settings
s = Settings(_env_file='.env')
print('llm_provider      =', repr(s.llm_provider))
print('openai_api_key    =', repr(s.openai_api_key))
print('openrouter_api_key=', repr(s.openrouter_api_key))
from ingestion.embeddings.provider import get_embedding_provider
print('provider factory:', get_embedding_provider(s.llm_provider).__class__.__name__)
EOF

llm_provider      = 'mock'
openai_api_key    = 'sk-your-key-here'
openrouter_api_key= ''
provider factory: MockEmbeddingProvider
```

The key `README.md` and `docs/SETUP.md` call required for AI features never gets set, and the configured provider is the mock — no AI calls at all.

**5. The code defines both keys.** `core/config.py:18-22` declares `llm_provider`, `openai_api_key`, `openrouter_api_key`, `openrouter_base_url`, and `openrouter_model`. One honesty note: `grep -rn "settings.llm_provider"` finds no reader of that field in the codebase — the OpenRouter fields are defined but not yet wired into a call path. So what the mismatch costs a newcomer today is what the steps above show: a required key with no line in the template, and an implied provider value outside the only set (`mock`/`openai`) the codebase's provider factory accepts — not a crash in the app itself.

### Expected

Per the issue: `README.md` and `.env.example` agree on which LLM API key a newcomer sets.

### Actual

At `f89c06f` they disagree exactly as described: the README/SETUP path leaves you with an undocumented key and, following the provider it implies (`openrouter`), a value the codebase's provider factory does not support; the `.env.example` path leaves the "required" key empty. I removed `.env` afterward; the tree is clean (`git status` empty, `.env` is gitignored).

Next step for me: propose the smallest fix that makes the two files agree — most likely adding `OPENROUTER_API_KEY` and an `openrouter` option to `.env.example` so it matches what the README and `core/config.py` already define — but I'll hold that for the PR discussion rather than assume it here.

(Disclosure: I drafted this report with AI assistance and read, ran, and edited every line myself.)

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run `--limit 3` (rubric v1, verifying the install): **3/3** — `agreement: 3/3 scored items` (pkg-01 accept, pkg-02 reject, pkg-03 accept, all agreeing).
2. First full run (rubric v1): **19/20** — `agreement: 19/20 scored items  (bar: 18/20: PASS)`. Only disagreement: pkg-03 (gold accept) graded reject on `environment-recorded` — the check demanded every deviation be acknowledged, and pkg-03's Arch-Linux run of a Kubuntu-filed issue names the OS but never calls it a deviation.
3. `--only pkg-03,pkg-06,pkg-11,pkg-16,pkg-20,calib-04 --include-calibration` after revision 1 (acknowledgment scoped to deviations that could change the answer): **5/5 scored** — `agreement: 5/5 scored items`, plus calib-04 agreeing reject. pkg-03 flipped to accept; pkg-16, pkg-06, pkg-20 held.
4. Second full run with `--save-run`: **19/20** — `agreement: 19/20 scored items  (bar: 18/20: PASS)`. pkg-03 now agreed, but pkg-01 (gold accept) flipped to reject on `environment-recorded` — the grader treated the report's unexplained `multidict 6.6.0` vs the thread's broken `6.5.0` as an unacknowledged load-bearing deviation. Same check, different false-fail: the trigger was too broad.
5. `--only pkg-01,pkg-03,pkg-06,pkg-11,pkg-16,pkg-20,calib-04 --include-calibration` after the restructure (`environment-recorded` = record exists and names the trigger's dimensions; the undermining-deviation reading moved to `evidence-bears-on-issue` as "a version far outside the issue's stated or confirmed range ... left unexplained"): **6/6 scored** — `agreement: 6/6 scored items`, plus calib-04. pkg-01 and pkg-03 both accept; pkg-16 held its reject under the new home.
6. Final full run with `--save-run beat-1-sandbox/unit-2/eval-run.txt`: **20/20** — `agreement: 20/20 scored items  (bar: 18/20: PASS)`, categories `clear-accept 8/8  disclosure 1/1  no-evidence 4/4  unfollowable-comms 3/3  wrong-target 4/4`. This is the agreement line in the committed `eval-run.txt`.

**Package analysis**

`pkg-16` (source `pandas-dev/pandas#66656`, "Passing a tuple at creation for 1-d index in df is fine but rename_axis with tuple fails"). Gold label: `reject` (category wrong-target). My rubric's verdict: `reject`, on `evidence-bears-on-issue`.

The candidate report reproduces the issue's exact code and shows the `ValueError: Length of new names must be 1, got 3` crash — and it looks convincing until you read its environment line against the issue's claim. The bundle's issue context says "The reporter confirmed the bug on the latest version and on the main branch (template checks ticked); the installed-versions block shows python 3.14.6 and a main-branch pandas build on macOS arm64." The candidate's own report states "Environment: pandas 1.5.3 (pip), Python 3.10.12, Ubuntu 22.04 (x86_64)" — pandas 1.5.3 is years behind latest/main, and the report never mentions the gap anywhere. Under my check's clause, that is "a version far outside the issue's stated or confirmed range, exercised with the difference left unexplained, so the artifact cannot speak to the reported bug" — the same read the gold note takes: "the shown ValueError is that old version's behavior, not evidence about the reported bug."

This is also the package my final check design exists for. In rubric v1, silent environment deviations lived in `environment-recorded` under a blanket "every deviation must be acknowledged" rule — which false-failed pkg-03 (Kubuntu→Arch on a platform-independent regex bug) and pkg-01 (multidict 6.5→6.6) in consecutive full runs. pkg-16 is what proved the family still needed a home: the version gap there isn't cosmetic, it is the whole problem — the artifact shows the old version's behavior, not the reported bug's. Moving the undermining-deviation case to `evidence-bears-on-issue` kept pkg-16's reject while releasing the two accepts, which is exactly the wrong-target shape this category was built around.

**Check rationale**

Quoted verbatim from the `rubric.md` uploaded to `tools/repro-check/`:

> | evidence-bears-on-issue | The report's artifacts — the quoted command outputs, logs, error text, observed states — each read against the behavior the issue describes (its actual/current-behavior lines and any maintainer trigger note in the thread). | The artifacts come from exercising the issue's question on a target the issue's claim covers: they either show the issue's described behavior (same symptom, error identity, or failure mode), or — on an honest cannot-reproduce — show a genuine run of the issue's trigger whose result the report states plainly. Fails when the artifacts show a different error or mechanism than the issue's and are presented as it, when they show only that the program starts or runs normally, when nothing quoted bears on the issue's behavior at all, or when the run silently targeted something the issue's claim does not cover — a version far outside the issue's stated or confirmed range, exercised with the difference left unexplained, so the artifact cannot speak to the reported bug. | required |

It reads this way because it has to hold four different wrong-target shapes at once without punishing honest attempts. The eval's wrong-target packages each attack from a different angle: pkg-02 runs a prefix range instead of the issue's offset-from-end syntax and gets an argument-validation error narrated as the capacity-overflow crash; pkg-08 modifies the expression so `$b` is unbound, producing a compile error presented as the issue's `Invalid path expression`; pkg-16 silently swaps the target version; pkg-17 shows garbled escape-sequence output with the terminal still alive as proof of a crash. One clause — "the artifacts come from exercising the issue's question" — covers all four, because in each case the quoted output answers a question the issue did not ask. The honest-cannot-reproduce branch exists because pkg-09 and pkg-10 are gold accepts: their artifacts show the trigger NOT firing, which is evidence too, as long as the report says so plainly. I rejected the obvious alternative — a separate "was the trigger faithful" check — because faithfulness can't be judged from the steps alone: pkg-02's steps *look* like they ran the issue's command; only reading the artifact against the issue's panic reveals the swap. The version sub-clause was the last piece added, in revision 3, after `environment-recorded` false-failed a different accept in two consecutive full runs.

**Trade-offs**

The check gives up precision on two edges, and I can name what each costs. First, "a version far outside the issue's stated or confirmed range" is a judgment phrase — a package tested on a moderately-different version with no comment could grade either way depending on how the grader reads "far." I accept that ambiguity deliberately: its predecessor was worse in a measurable way. Requiring explicit acknowledgment of *every* load-bearing deviation produced a false-fail in two out of two full runs (pkg-03's unremarked Kubuntu→Arch delta, then pkg-01's unremarked multidict 6.5.0→6.6.0 delta — the grader decided the thread-named dependency was load-bearing). Narrowing the clause to deviations that leave the artifact unable to speak to the reported bug fixed both, verified by the `--only` canary runs in my history (pkg-01, pkg-03 accept; pkg-16, pkg-06, calib-04 still reject; pkg-20 held as the disclosure canary each time). Second, the "left unexplained" qualifier means a report that *does* acknowledge a big version gap but still claims confirmation passes this check — it then fails on `outcome-honest` instead, which is the defense-in-depth the check set is supposed to provide (pkg-17 over-generalizes to the Store release and is caught by that check plus this one). Nothing else in the set moved when the clause landed: the six-canary `--only` run before the confirming full run was clean, and the committed run is 20/20 with every category at 100%.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
