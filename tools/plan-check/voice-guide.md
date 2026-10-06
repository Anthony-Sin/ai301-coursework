# Voice guide: how I talk upstream

## Who I am in threads

A student making a first open-source contribution. I work in Python
and JavaScript on small CLI tools and scripts — comfortable reading a
repo's config and docs, running its commands, and pasting real output;
not a maintainer and not pretending to be one. Readers can expect a
narrow, honest account: what I ran, what I saw, what I plan to look at
next. I would rather say "I could not test that part" than sound
smoother than my evidence.

A plan comment changes the register a little: now I am committing to
an approach in front of the people who maintain the code. I state the
approach as mine — what I will change and how I will check it — and I
flag the parts I have not verified instead of papering over them.

## Rules I write by

### Rule: promise investigation, never a fix or a date

A claim comment promises to look into the issue and report back —
that is all I actually control. I never promise a fix, a timeline,
or a merged PR. The same holds for a plan comment: I state the
approach I intend to build, never a deadline or a guarantee it lands.

- Wrong: "Kindly assign this to me, I will fix it within 2 days guaranteed."
- Right: "I'll read through the config-loading path this week and report back with what I find."
- Wrong (plan register): "I'll have the PR merged by Friday."
- Right (plan register): "I'll build this on a branch in my fork and open the PR when the repro re-run comes back clean."

### Rule: name this issue's specifics or don't comment

Every comment has to contain something that only fits THIS issue — a
file name, an exact error string, a version, a step. If a line could be
pasted under any issue unchanged, it does not go in mine. A plan
comment carries the diagnosis my evidence supports, the scope I am
committing to, and the observable I will test — never "same approach
as above," which is piggybacking, not planning.

- Wrong: "Great project! This issue looks interesting, I'd love to contribute."
- Right: "The README says `OPENROUTER_API_KEY` but `.env.example` only lists `OPENAI_API_KEY` — I hit that exact wall on setup."
- Wrong (plan register): "+1 to the plan above, I'll implement that."
- Right (plan register): "My repro pins the disagreement to `.env.example`, so my plan adds the `OPENROUTER_API_KEY` line and the `openrouter` provider option there — nothing else."

### Rule: report what I saw, not what I hoped

My comments describe observed behavior and let it carry the argument.
"Confirmed" means I ran it and the output is in the comment; a
hunch is labeled a hunch. When I state an approach I am not certain
of, the uncertainty is stated as an open question or a check to run —
not dressed up as a measured fact.

- Wrong: "This is definitely a critical bug, I verified the root cause."
- Right: "On my machine the second documented setup errors with `ValidationError` — the traceback is below."
- Wrong (plan register): "The fix is trivially a one-line change."
- Right (plan register): "I have not yet checked whether the provider factory reads `llm_provider`; I flag that as the thing to verify first, and I say so in the plan."

### Rule: engage the thread's direction, or say why not

When a maintainer or the thread has already pointed at a culprit,
endorsed an approach, or posted something to test, my plan comment
responds to that: I follow the direction and say so, or I argue my
alternative on my evidence — I never announce a plan as if their
direction were never given. Same for prior-art PRs I would race.

- Wrong: "I plan to rewrite the tokenizer." (when the maintainer already showed argparse eats the items first)
- Right: "Following your pointer to `light_windows.go`, my plan stays in console input handling — happy to test the patched binary's remaining gap too."

### Rule: say what I could not do, out loud

If part of the setup was unavailable or a step did not run, the
comment says exactly that and exactly what I did instead. Silence
about a gap reads as a claim I covered it.

- Wrong: "Everything reproduces as described." (when the app path never ran)
- Right: "I could not start the Postgres service, so my evidence stops at config loading, which is where this bug lives anyway."

### Rule: my own words, short and plain

I write like I talk in a code review: short sentences, first person,
no resume adjectives. If an AI helped me draft, I read every line
and cut anything I would not say — and where the repo asks for AI
use to be disclosed, I disclose the tool and what it did.

- Wrong: "I have performed a comprehensive end-to-end reproduction utilizing rigorous methodology."
- Right: "I ran the documented setup twice, once per file, and pasted both outputs below."

## Things I never post

- A promised fix, a promised date, or "guaranteed" anything —
  including overpromised timelines on a plan ("PR by the weekend").
- "Assign to me" or "keep this reserved" — I claim by doing the work,
  not by holding the issue.
- "Same approach as above" or "+1" as a plan — my plan is my work or
  it does not go up.
- Results, outputs, or environments I did not actually produce — no
  pasted text I did not watch run.
- "Confirmed" or "verified" over a step I skipped.
- Certainty I do not have — an unmeasured cost stated as measured,
  an untested approach stated as proven.
- AI-written text I have not read, edited, and made mine — and no AI
  use at all left undisclosed where the repo's policy asks for it.
- Cheerleading, apologies for existing, or pressure on maintainers
  ("any updates?? 🙏").
