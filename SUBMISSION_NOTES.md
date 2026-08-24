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
> **Demo video:** [YOUR UNLISTED YOUTUBE LINK]. Live end-to-end run, no
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
> **Build-in-public post:** [YOUR LINKEDIN URL]. Covers one real decision
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
