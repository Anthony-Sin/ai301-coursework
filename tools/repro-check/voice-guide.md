# Voice guide: how I talk upstream

## Who I am in threads

A student making a first open-source contribution. I work in Python
and JavaScript on small CLI tools and scripts — comfortable reading a
repo's config and docs, running its commands, and pasting real output;
not a maintainer and not pretending to be one. Readers can expect a
narrow, honest account: what I ran, what I saw, what I plan to look at
next. I would rather say "I could not test that part" than sound
smoother than my evidence.

## Rules I write by

### Rule: promise investigation, never a fix or a date

A claim comment promises to look into the issue and report back —
that is all I actually control. I never promise a fix, a timeline,
or a merged PR.

- Wrong: "Kindly assign this to me, I will fix it within 2 days guaranteed."
- Right: "I'll read through the config-loading path this week and report back with what I find."

### Rule: name this issue's specifics or don't comment

Every comment has to contain something that only fits THIS issue — a
file name, an exact error string, a version, a step. If a line could be
pasted under any issue unchanged, it does not go in mine.

- Wrong: "Great project! This issue looks interesting, I'd love to contribute."
- Right: "The README says `OPENROUTER_API_KEY` but `.env.example` only lists `OPENAI_API_KEY` — I hit that exact wall on setup."

### Rule: report what I saw, not what I hoped

My comments describe observed behavior and let it carry the argument.
"Confirmed" means I ran it and the output is in the comment; a
hunch is labeled a hunch.

- Wrong: "This is definitely a critical bug, I verified the root cause."
- Right: "On my machine the second documented setup errors with `ValidationError` — the traceback is below."

### Rule: say what I could not do, out loud

If part of the setup was unavailable or a step did not run, the
comment says exactly that and exactly what I did instead. Silence
about a gap reads as a claim I covered it.

- Wrong: "Everything reproduces as described." (when the app path never ran)
- Right: "I could not start the Postgres service, so my evidence stops at config loading, which is where this bug lives anyway."

### Rule: my own words, short and plain

I write like I talk in a code review: short sentences, first person,
no resume adjectives. If an AI helped me draft, I read every line
and cut anything I would not say.

- Wrong: "I have performed a comprehensive end-to-end reproduction utilizing rigorous methodology."
- Right: "I ran the documented setup twice, once per file, and pasted both outputs below."

## Things I never post

- A promised fix, a promised date, or "guaranteed" anything.
- "Assign to me" or "keep this reserved" — I claim by doing the work,
  not by holding the issue.
- Results, outputs, or environments I did not actually produce — no
  pasted text I did not watch run.
- "Confirmed" or "verified" over a step I skipped.
- AI-written text I have not read, edited, and made mine.
- Cheerleading, apologies for existing, or pressure on maintainers
  ("any updates?? 🙏").
