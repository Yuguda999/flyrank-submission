# Retrospective

*Written for the version of me who started this track.*

---

## What I set out to do

I came in wanting a portfolio, assuming the work was done and this was just
packaging — I'd shipped real systems, I only needed somewhere to put them.
I was wrong about which part was hard, and wrong about what I was selling.

## What changed

**I was calling myself the wrong thing.** I started as "backend engineer who
does AI." Halfway through I rebuilt the site as a machine learning engineer
portfolio — not because it sounded better, but because when I listed what I
actually spend time on (LLM reasoning pipelines, retrieval over messy
documents, evaluation harnesses, serving open-weight models) the backend
framing was describing the substrate instead of the work. It meant rewriting
every case study. Worth it.

**My proof was invisible.** I sent the site to a backend dev and asked two
questions before showing him anything else: in ten seconds, what do I do,
and would you believe I'm good at it. He got the first. On the second:
"cautiously yes, but I haven't seen a single number." He was right, and it
was worse than he knew — CampusPQ's 5,000+ processed questions at 98% had
been on my CV for months and never made it onto my own site. He also caught
what I'd have defended if asked less bluntly: I'd led with my capstone, a
tool with exactly one user (me), under a headline claiming "systems that
ship," while the thing that actually shipped got one clause and a link to a
different domain. I had inverted my own evidence. The fix took an afternoon.
Noticing was the hard part, and I didn't.

**I stopped trusting things that look fine.** Three times this track,
something that looked correct wasn't, and only measuring caught it:

- My section-label grey failed WCAG contrast at 4.47 against a 4.5 minimum.
  It looked completely fine. Eyes don't measure ratios.
- My agent's eval suite passed in place and failed from a fresh clone: the
  config file was clobbering environment variables, silently making every
  documented override a no-op for anyone who had a config — which was
  everyone who followed my own setup instructions.
- My contact form started failing after rapid submissions. I wrote it up as
  "seems to be throttling, hadn't recovered." My reviewer pushed back:
  *that's not a known limitation, that's an open incident.* Measured, it was
  two different failures wearing the same mask — a 429 that clears in four
  minutes, and a 404 from stale form registration that a redeploy fixes.

## The three most transferable things

**1. Put the guardrail in the architecture, not the instructions.**
The obvious way to build my agent was to let the model run git commands and
interpret them live. Instead a deterministic script produces one blob of
ground truth and the model may only summarise it. "Don't invent activity"
stops being a rule the model might drift from and becomes a fact about the
system — it cannot report a commit that isn't there, because one that isn't
there never enters its context. Same for safety: the script uses only
read-only git, so "never modify my repos" isn't trust, it's the absence of a
code path.

**2. Ask for the criticism blind, and don't defend.**
I sent the link with two questions and *nothing else* — no proof statement,
no context — because if I'd told him what the site was supposed to say, his
ten-second read would just be him reading it back to me. Then I sat on my
hands. Every instinct said explain why the email was in the footer. That
explanation would have cost me the finding.

**3. Test from outside your own setup.**
Everything that broke, broke at the boundary between my machine and someone
else's: a config that only worked in my shell, a script that only passed in
my own directory, an export in `.bashrc` that agent runtimes never read
because they spawn non-interactive shells. "Works on my machine" isn't a
joke about laziness — it's a specific, predictable class of bug, and the fix
is cheap: run it from a fresh clone, in a clean environment, as a stranger
would.

## What I'd build next

The orchestrator upgrade I specced and deliberately did not ship. My FL-04
pipeline is still a workflow — the sequence is hardcoded, the model doesn't
choose. Making it route on a diff-size threshold, so trivial changes skip
the red-team step entirely, is the honest next move. I labelled it "designed,
not built" on the site rather than calling it agentic, and I'd rather close
that gap than keep explaining it.

Second: my strongest case study still has no screenshot, because it's client
work. No amount of writing fixes that. I need to build something equivalent
that's mine to show.
