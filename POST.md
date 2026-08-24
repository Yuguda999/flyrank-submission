# Build-in-public post

*For LinkedIn. Trim the middle if it runs long for the platform.*

---

I just finished a 10-week AI fluency track. The thing I actually built is
small: an agent that sweeps my eight git repos once a week and writes me a
one-page digest — what shipped, what's gone stale, what I left uncommitted.

The interesting part isn't the tool. It's one decision and one thing that
went wrong.

**The decision.**

The obvious way to build it was to let the model run the git commands itself
— four per repo, interpret them live, write the summary. I didn't do that.

Instead a plain bash script runs all the git commands and prints one block of
output, and the model's only permitted job is to summarise *that block*.

The difference is where the guardrail lives. If the model runs the commands,
"don't invent activity that didn't happen" is an instruction — and
instructions drift. With the script in front, it's a property of the system:
the model cannot report a commit that isn't there, because a commit that
isn't there never enters its context. Same for safety. The script uses only
read-only git subcommands, so "never modify my repos" isn't trust, it's the
absence of a code path that could.

I keep coming back to that framing now. When you want a guarantee from
something non-deterministic, put the constraint in the architecture, not in
the prompt.

**The thing that went wrong.**

My eval suite passed. Fifteen cases, all green. Then I cloned the repo to a
temp directory and ran the same suite on the same machine — and two cases
failed.

The config file was being sourced with plain assignments, which clobbered
environment variables instead of yielding to them. So every per-run override
I'd documented in my own README — `STALE_DAYS=60 ...` — was silently a no-op
for anyone who had a config file. Which was everyone who followed my setup
instructions.

It passed in place and failed from a clone. That gap is the entire distance
between "works on my machine" and "a stranger can run this," and the only
reason I found it is that I ran the tests the way a stranger would rather
than the way that was convenient.

**One more, since honesty is the point.**

I also asked a backend dev for a blind crit of my portfolio — link and two
questions, no context, because if I'd told him what the site was supposed to
say he'd just have read it back to me. He got what I do in ten seconds. Then:
"cautiously yes, but I haven't seen a single number."

He was right, and worse than he knew. A metric from a system I shipped —
5,000+ processed questions at a 98% success rate — had been sitting on my CV
for months and had never made it onto my own site. I'd also led with my
capstone, a tool with exactly one user (me), under a headline claiming
"systems that ship," while the thing that actually shipped got one clause and
a link somewhere else. I had inverted my own evidence and couldn't see it.

The fix took an afternoon. Noticing was the hard part, and I didn't notice.

---

The agent: github.com/Yuguda999/weekly-review-agent
The portfolio: yuguda999.github.io/ys-dev

Built with Claude. The code is mostly Claude's; the decision about what the tool
is allowed to do, and the testing that caught the bugs, are mine — and that
turned out to be the part that mattered.
