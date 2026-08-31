# FlyRank AI Fluency — Final Submission

**Yuguda Muhammed Shamsudeen** · Machine Learning Engineer · Lagos, Nigeria
elemenx93@gmail.com · [GitHub](https://github.com/Yuguda999) · [LinkedIn](https://linkedin.com/in/yuguda)

Everything I built on this track, in one place.

---

## The one-line claim

> **I build models that survive production.**

---

## Start here

| | Link |
|---|---|
| **Portfolio (live)** | https://yuguda999.github.io/ys-dev/ · https://yuguda.netlify.app/ |
| **Capstone agent** | [weekly-review-agent](https://github.com/Yuguda999/weekly-review-agent) |
| **Retrospective** | [RETROSPECTIVE.md](RETROSPECTIVE.md) |
| **Build write-up** | [BUILD_WRITEUP.md](BUILD_WRITEUP.md) |
| **Capstone demo (3m26s)** | [youtu.be/rFYE0ezQ6jY](https://youtu.be/rFYE0ezQ6jY) |
| **Build-in-public post** | [LinkedIn](https://www.linkedin.com/feed/update/urn:li:ugcPost:7499843400519688192/) · [draft](POST_LINKEDIN.txt) |

---

## Capstone — Weekly Repo Review Agent

A personal agent that sweeps every git repo I work in weekly and writes a
one-page digest. Built so the model **cannot invent activity**: a
deterministic bash script gathers the git data, and the agent is only
permitted to summarise what that script actually printed.

| Item | Where |
|---|---|
| Repo, README, setup, architecture | [weekly-review-agent](https://github.com/Yuguda999/weekly-review-agent) |
| Eval suite — 15 cases, builds its own fixtures | [`evals/run-evals.sh`](https://github.com/Yuguda999/weekly-review-agent/blob/main/evals/run-evals.sh) |
| Eval results & limitations | [README § Eval results](https://github.com/Yuguda999/weekly-review-agent#eval-results-v2) |
| Where AI did the work | [README § Where AI did the work](https://github.com/Yuguda999/weekly-review-agent#where-ai-did-the-work) |
| Design spec (written before building) | [06-agent-design-spec.pdf](deliverables/06-agent-design-spec.pdf) |
| Demo video (3–5 min, live run) | [youtu.be/U7sRo703ZFI](https://youtu.be/U7sRo703ZFI) |

Run it yourself:

```bash
git clone https://github.com/Yuguda999/weekly-review-agent.git
cd weekly-review-agent && bash install.sh
$EDITOR ~/.config/weekly-review/config   # set GH_USER
claude                                    # then: /weekly-review
```

---

## Portfolio

Live at **https://yuguda999.github.io/ys-dev/**. Five pages, four case
studies, one action (email for a technical screening).

| Case | Status | Page |
|---|---|---|
| Proposal Generation Engine | In production · 30% → 90%+ output quality under an eval harness | [proposal.html](https://yuguda999.github.io/ys-dev/proposal.html) |
| FL-04 Orchestrator | Pipeline live, agent designed | [fl04.html](https://yuguda999.github.io/ys-dev/fl04.html) |
| CampusPQ | Live · 5,000+ questions at 98% | [campuspq.html](https://yuguda999.github.io/ys-dev/campuspq.html) |
| Project Edix | Deployed on Cardano preprod | [edix.html](https://yuguda999.github.io/ys-dev/edix.html) |

---

## Every deliverable, by week

| Week | Deliverable | File |
|---|---|---|
| 5 | Portfolio live + real reviewer reaction + "still ugly" list | [05-portfolio-live-and-reviewed.pdf](deliverables/05-portfolio-live-and-reviewed.pdf) |
| 6 | Agent design spec — job, tools, 5 pre-build eval cases, guardrails, platform justification | [06-agent-design-spec.pdf](deliverables/06-agent-design-spec.pdf) |
| 6 | DNS walkthrough — CNAME, resolvers, nameservers, in plain words | [06-dns-walkthrough.pdf](deliverables/06-dns-walkthrough.pdf) |
| 6 | "Explain it like you built it" — the stale-branch dedup bug, in my own words | [06-explain-it-like-you-built-it.pdf](deliverables/06-explain-it-like-you-built-it.pdf) |
| 7 | Mobile fix log — what was broken on a real phone, what changed | [07-mobile-fix-log.pdf](deliverables/07-mobile-fix-log.pdf) |
| 7 | Design review — feedback, must-fix/nice-to-have sort, what I changed | [07-design-review-response.pdf](deliverables/07-design-review-response.pdf) |
| 8 | Contact form — the one dynamic feature, plus a plain-words explainer of the data flow | [08-contact-form-explainer.pdf](deliverables/08-contact-form-explainer.pdf) |
| 9 | "Where it breaks" — hardening: 5 fixes, 4 named limitations, speed numbers, review response | [09-where-it-breaks.pdf](deliverables/09-where-it-breaks.pdf) |
| 9 | Plan to keep building — how to add the next case, next piece named, cron reminder | [09-plan-to-keep-building.pdf](deliverables/09-plan-to-keep-building.pdf) |
| 9 | Identity kit + content map — claim, sections, palette with hex codes, favicon, rejection note | [09-identity-kit-and-content-map.pdf](deliverables/09-identity-kit-and-content-map.pdf) |
| 10 | Retrospective | [RETROSPECTIVE.md](RETROSPECTIVE.md) |
| 10 | Build write-up — stack and why, hardest break, what's next | [BUILD_WRITEUP.md](BUILD_WRITEUP.md) |
| 10 | Capstone demo — live portfolio walkthrough, working contact form, where AI did the heavy lifting | [youtu.be/rFYE0ezQ6jY](https://youtu.be/rFYE0ezQ6jY) |
| 10 | Build-in-public post | [LinkedIn post](https://www.linkedin.com/feed/update/urn:li:ugcPost:7499843400519688192/) |

---

## Where AI did the work

I built all of this with Claude, and the honest split is worth stating.

AI wrote most of the code and most of the first drafts. What I own is the
judgement: the decision to make the agent's guardrail structural rather than
instructional, the choice to reposition from backend engineer to ML engineer,
the call on which images to reject, and — the part that mattered most — the
testing that caught what looked fine and wasn't.

Three things AI wrote that I caught by checking: a config-precedence bug that
only failed from a fresh clone, a contrast value that failed WCAG at 4.47
against a 4.5 minimum, and a stale-branch counter that reported one commit
twice. Per-project detail is in each README.

---

## Known gaps

- **FlyRank subdomain not live.** `yuguda.flyrank.ai` returns NXDOMAIN —
  subdomains are provisioned after capstone approval, and per the portal
  Q&A verification lands mid-September. The site is live on two public
  HTTPS URLs in the meantime, and the DNS walkthrough above is the
  checklist I'll run when the record exists.
- **Graduate badge is a placeholder.** In the footer, marked
  `data-placeholder`, pending the real verification URL.
- My strongest case study has no screenshot — it's client work.
