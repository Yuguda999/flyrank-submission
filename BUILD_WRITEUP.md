# Build write-up

**Site:** https://yuguda.netlify.app · **Source:** github.com/Yuguda999/ys-dev
**Capstone agent:** github.com/Yuguda999/weekly-review-agent

---

## The stack, and why

**Hand-written static HTML, CSS and JavaScript. No framework, no build step,
no dependencies.**

This was a deliberate constraint, not laziness. One of the pass criteria on
this track was being able to explain every file I deployed, and the fastest
way to guarantee that is for there to be no generated code in the site at
all. There is no bundler output I'd have to reverse-engineer, no framework
conventions I'd be repeating without understanding. Five HTML pages, one
stylesheet with the palette at the top as CSS custom properties, two small
JS files. I can open any of them and account for every line.

The trade is real: no component reuse, so the nav and footer are duplicated
across five pages, and changing one means changing five. At this size that's
cheaper than the alternative. At twenty pages it wouldn't be.

**Netlify for hosting, GitHub Pages as a mirror.** Netlify because the one
dynamic feature — the contact form — needs something server-side to catch a
POST, and Netlify Forms provides that on the free tier with no server for me
to run or pay for. It parses my HTML at deploy time, finds the form, and
starts accepting submissions. GitHub Pages can't do that at any price, which
is why Netlify is the canonical origin and the Pages copy carries a
`rel="canonical"` pointing at it.

**Claude Code as the agent runtime** for the capstone, over a hosted
assistant with connectors. It has native shell and filesystem access, which
is the whole job — the agent reads local git repos. A hosted connector would
have meant giving a third party repo access to do something my own machine
can already do.

**The one architectural decision I'd defend hardest:** in the agent, a
deterministic bash script gathers all the git data and the model is only
permitted to summarise what that script printed. The obvious build lets the
model run the git commands itself. I rejected it because "don't invent
activity that didn't happen" is a weaker guarantee as an instruction than as
a property of the system. With the script in front, the model *cannot*
report a commit that isn't there — one that isn't there never enters its
context. Read-only git subcommands mean "never modify my repos" isn't trust
either; there's no code path that could.

---

## The hardest thing that broke

**I published my entire commit history to the internet without noticing.**

My deploy process was dragging the project folder onto Netlify Drop. That
uploads everything in the folder — including `.git`. For some period,
`https://yuguda.netlify.app/.git/config` returned HTTP 200, and with it the
full commit history was downloadable by anyone who guessed the path. Nothing
in the UI warns you. The site looked perfect.

I found it by probing my own site for things that shouldn't be there rather
than checking that the things that should be there worked.

The fix wasn't "remember not to do that." I wrote a build script that copies
only intended files into a separate `dist` directory, so the folder I drag
physically cannot contain `.git`. Later I replaced even that with
`git archive HEAD`, which exports tracked files only — the guarantee comes
from the tool, not from my memory. Same principle as the agent's guardrail:
if you want to be sure, make the bad state unrepresentable.

The same instinct caught two more later. A raw AI chat transcript containing
my account UUID was being served publicly from the portfolio because it
happened to sit in the repo folder. And on the last day of the build I found
my two public URLs had silently drifted into two *different sites* — GitHub
Pages had the current design but no contact form, Netlify had the form but
predated a contrast fix. A visitor got a different portfolio depending on
which link they followed. Both were found by checking, not by luck.

---

## What I'd build next

**The orchestrator upgrade I specced and deliberately didn't ship.** My FL-04
pipeline is still a workflow: draft, red-team, revise, in a hardcoded
sequence, with the model choosing nothing. The design is to route on a
diff-size threshold so a trivial change skips the red-team step entirely and
a large one pulls in extra context first. I labelled it "designed, not built"
on the site rather than calling it agentic, and closing that gap is the
honest next move.

**Second: a shippable case study I own outright.** My strongest project — the
Proposal Generation Engine, the one with the 30% → 90%+ quality improvement
under an evaluation harness — is client work, so it's the only case on the
site with no screenshot. That's a real hole no amount of writing fixes. I
need to build something equivalent that's mine to show.
