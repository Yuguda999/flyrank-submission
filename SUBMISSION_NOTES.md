# Submission notes — paste into the portal Notes field

---

## For Assignment 8.1 (FL-09 — Documentation and demo)

> **Capstone:** Weekly Repo Review Agent — a personal agent that sweeps every
> git repo I work in weekly and writes a one-page digest.
>
> **README:** github.com/Yuguda999/weekly-review-agent — covers what it does
> and for whom, setup a stranger can follow (clone → `install.sh` → set one
> config value → run), usage examples with real output, an architecture
> sketch, v2 eval results, and the limitations list.
>
> **Reproducibility was tested, not assumed.** I cloned the repo to a temp
> directory, installed into a clean fake home, and ran the setup as a
> stranger would. That caught a real bug: sourcing the config file clobbered
> environment variables instead of yielding to them, which silently made
> every documented per-run override a no-op for anyone who had a config
> file. It passed in place and failed from a clone. Fixed, and E-numbered in
> the suite.
>
> **Evals:** 15 cases, all passing. The suite builds its own throwaway git
> repos with controlled history, so it never touches real ones. Two cases
> went red while I was writing it — one bad assertion of mine, and the
> precedence bug above — and both are documented in the README rather than
> quietly removed. A suite that has never failed hasn't been tested either.
>
> **Limitations are in the README, not hidden:** one user, local-only (never
> calls the GitHub API, so it cannot see PRs, issues or CI), ownership is a
> string comparison against a GitHub username, "stale" is time-only and
> doesn't check merge status, manual trigger, and bash 4+ so stock macOS
> bash 3.2 fails.
>
> **Where AI did the work** is its own README section. Short version: Claude
> wrote most of the code and first drafts; the architectural decision — put
> the guardrail in the system rather than the prompt — was mine, and so was
> the testing that caught three bugs AI introduced.
>
> **Demo video:** https://youtu.be/U7sRo703ZFI. Live end-to-end run, no
> slides. Explains the design decision (deterministic script feeding the
> model, so it cannot invent activity) and one limitation on camera
> (local-only — no GitHub API, so PRs and CI are invisible to it).

---

## For Assignment 8.2 (FL-10 — Final package and retrospective)

> **Submission package:** github.com/Yuguda999/flyrank-submission — index
> README linking every deliverable from the whole track, plus the 10
> assignment PDFs in `deliverables/`.
>
> **Retrospective:** RETROSPECTIVE.md in that repo (796 words).
>
> **Live portfolio:** yuguda999.github.io/ys-dev and yuguda.netlify.app —
> five pages, four case studies, one action.
>
> **Build-in-public post:** https://www.linkedin.com/feed/update/urn:li:ugcPost:7499843400519688192/. Covers one real decision
> (putting the agent's guardrail in the architecture instead of the
> instructions) and one real limitation (my eval suite passed in place and
> failed from a fresh clone — the gap between "works on my machine" and "a
> stranger can run this").
>
> **On the FlyRank domain criterion — flagging rather than claiming it.**
> `yuguda.flyrank.ai` currently returns NXDOMAIN. My understanding from the
> track material is that subdomains are provisioned after the capstone is
> approved, and the portal Q&A (17 Aug) says verification and graduate
> badges are issued mid-September. So this is sequencing, not something
> outstanding on my side.
>
> What is ready for the moment the record exists: the site is live over
> HTTPS on two public URLs with automatic certificates, hosted on Netlify,
> which accepts a custom domain without a rebuild. I wrote the DNS
> walkthrough in Week 6 specifically so this would be a checklist rather
> than research — it's in the package as
> `deliverables/06-dns-walkthrough.pdf`, and covers what a CNAME is, the
> exact value mine will hold, and the resolver → nameserver → record →
> response path end to end. When Ops creates the record I add the custom
> domain in Netlify, wait for propagation, and confirm the padlock.
>
> The graduate badge is installed in my site footer but points at the course
> homepage, marked `data-placeholder` in the markup, pending the real
> verification URL for the same reason.
>
> Happy to complete both the moment the subdomain and verification link are
> issued, and to resubmit for sign-off then if that's cleaner.

---

## For Week 10 Capstone (Send the Link: Launch, Demo & Story)

> **1. The launched portfolio** — https://yuguda.netlify.app
> Five pages, four case studies, one action (contact for a technical
> screening). One claim: *I build models that survive production.* Also
> mirrored at yuguda999.github.io/ys-dev, which carries `rel=canonical`
> pointing at the Netlify origin — that's the only host where the contact
> form's POST handler exists.
>
> **2. The proof (build-in-public story)** —
> https://www.linkedin.com/feed/update/urn:li:ugcPost:7499843400519688192/
> One real win: putting the agent's guardrail in the architecture rather
> than the prompt, so it cannot invent activity by construction. One real
> limitation: my eval suite passed in place and failed from a fresh clone,
> because the config file was clobbering environment variables and silently
> made every documented override a no-op for anyone following my own setup
> instructions.
>
> **3. The package**
> - Demo (3m26s, live, no slides): https://youtu.be/rFYE0ezQ6jY
> - Build write-up: github.com/Yuguda999/flyrank-submission/blob/main/BUILD_WRITEUP.md
>   — the stack decision (hand-written static HTML so every deployed file is
>   explainable; Netlify because GitHub Pages cannot process a form at any
>   price), the hardest break, and what I'd build next.
> - Plan to keep building: `deliverables/09-plan-to-keep-building.pdf` —
>   next piece named (DevMemory), with a live monthly cron reminder on my
>   machine (`crontab -l` shows it) rather than an intention.
>
> **The hardest break, since it's the honest part:** my deploy process was
> dragging the project folder onto Netlify Drop, which uploads everything in
> it — including `.git`. For a period `/.git/config` returned HTTP 200 and my
> whole commit history was publicly downloadable. Nothing warns you; the site
> looked perfect. I found it by probing my own site for things that should
> not be there. The fix wasn't "remember not to do that" — it's
> `git archive HEAD`, which exports tracked files only, so the folder I
> deploy physically cannot contain `.git`. The same instinct later caught a
> chat transcript with my account UUID being served publicly, and — on the
> last day — that my two public URLs had drifted into two different sites,
> one with the contact form and one without.
>
> **4. The FlyRank loop** — the graduate badge is installed in the footer but
> currently points at the course homepage, marked `data-placeholder` in the
> markup, because verification pages are issued mid-September per the portal
> Q&A. Same reason `yuguda.flyrank.ai` is still NXDOMAIN. The DNS walkthrough
> in `deliverables/06-dns-walkthrough.pdf` is the checklist I'll run the
> moment the record exists — Netlify accepts a custom domain with no rebuild.
> Happy to be featured as a case study.
