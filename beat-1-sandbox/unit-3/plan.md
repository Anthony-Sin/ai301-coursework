# Plan: make `README.md` and `.env.example` agree on the LLM key (#73)

## Diagnosis

From my reproduction posted above: at `f89c06f`, `README.md` (Quick
Start) and `docs/SETUP.md` both instruct a newcomer to add
`OPENROUTER_API_KEY` to `.env`, but the `.env.example` those docs say
to copy carries no `OPENROUTER_API_KEY` line, and its `LLM_PROVIDER`
comment offers only `mock` and `openai`. `core/config.py` defines the
full OpenRouter field set (`openrouter_api_key`, `openrouter_base_url`,
`openrouter_model`) next to `openai_api_key`, so the code side already
knows OpenRouter — the template is the side that disagrees, not the
README. The issue asks to "make the two files agree."

The smallest change that makes them agree is bringing `.env.example`
in line with what the README, SETUP, and `core/config.py` already
describe. The alternative — editing README and SETUP to drop
OpenRouter — is two files rewritten against three sources pointing
the other way, and it would silently change the provider the
documented setup teaches.

## Scope

In scope: `.env.example` only — the `LLM_PROVIDER` options comment
and the API-key block.

Not in scope: `README.md` and `docs/SETUP.md` (already consistent
with the chosen direction); `core/config.py` (already defines the
fields); any wiring of `llm_provider` into a provider call path — the
field has no reader today (my repro, step 5), and whether OpenRouter
should be exposed before anything consumes it is a maintainer call I
flag below, not part of this change.

## Changes

1. `.env.example`, LLM provider comment: add `openrouter` to the
   listed options alongside `mock` and `openai`.
2. `.env.example`: add `OPENROUTER_API_KEY=` under `OPENAI_API_KEY`,
   commented as required when `LLM_PROVIDER=openrouter` — the key the
   README and SETUP tell the newcomer to set.
3. `.env.example`: add commented `# OPENROUTER_BASE_URL=` and
   `# OPENROUTER_MODEL=` lines noting that defaults come from
   `core/config.py`, so a newcomer sees the full OpenRouter surface
   without being forced to fill it.

No code changes; no test-file changes — this is a docs/template
consistency fix.

## Test plan

Re-run my reproduction steps on the branch and report before/after:

1. `cp .env.example .env`, then `grep -c OPENROUTER_API_KEY .env` —
   `0` before the change, `1` after.
2. `.env` written with the README's implied OpenRouter settings
   (`LLM_PROVIDER=openrouter`, `OPENROUTER_API_KEY=sk-or-...`): load
   `core/config.py`'s `Settings` in the same throwaway venv —
   `llm_provider` is `openrouter` and `openrouter_api_key` is
   populated. The fields already existed; now a newcomer who copies
   the file the docs name can actually reach them.
3. `grep -n "OPENROUTER\|LLM_PROVIDER" README.md docs/SETUP.md
   .env.example` — all three files name the same provider set:
   `mock`, `openai`, `openrouter`.
4. Control: `.env.example` copied unchanged still resolves
   `llm_provider` to `mock` — the default path is untouched.

## Risks / open questions

- `settings.llm_provider` has no reader in the codebase today, and
  the only provider factory (`ingestion/embeddings/provider.py`)
  accepts only `mock`/`openai` — exposing `openrouter` in the
  template does not make the app call it. Flagged for review: if
  maintainers would rather have the docs match the wired-up
  providers, the reverse fix (README/SETUP updated to drop OpenRouter)
  is a direction change, not more work — but README + SETUP +
  `config.py` pointing at OpenRouter is why I picked this side.

## Deviations

Nothing structural changed: the built change is the `.env.example`
edit the plan named — the `openrouter` option in the `LLM_PROVIDER`
comment, the `OPENROUTER_API_KEY` line, and the commented
`OPENROUTER_BASE_URL`/`OPENROUTER_MODEL` lines. One cosmetic detail:
the plan wrote `OPENROUTER_API_KEY=` empty, and the committed line
carries the `sk-or-your-key-here` placeholder to match the existing
`OPENAI_API_KEY=sk-your-key-here` style.
