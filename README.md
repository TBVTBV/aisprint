# AI Sprint 2026 — Pediatric Pulmonology Pre-Visit Intake

> HCI Master's · AI Product Sprint 2026 · Team repo
>
> **Challenge #6 — Incomplete, Unstructured, or Hard-to-Access Medical Information (Pediatric Pulmonology)**

This repository holds our team's work for the AI Product Sprint. Our challenge: a large share of every pediatric pulmonology visit is spent reconstructing a child's clinical history — symptoms, inhaler use, prior hospitalisations, treatment responses, and environmental exposures — from partial, unstructured input, because families often don't know which details matter. **We are focusing on the moment *before* the visit: how history is collected from families as pre-visit intake, and why it reaches the clinician incomplete.**

## Team

- Matan Rosen
- Anat Katzir
- Gal Yeshayahu
- Mikhail Yagudaev

## Current status — as of 24 July 2026

- ✅ **Challenge selected and scoped** to pre-visit intake (vs. point-of-care capture or the whole journey).
- ✅ **Desk research done** — documentation/history-taking burden, existing tools (c-ACT), environmental-trigger under-reporting, proxy-report limitations. Findings feed the Research Plan background.
- ✅ **Research Plan v1 drafted & committed** — see [`Research_Plan_Pediatric_Pulmonology.md`](./Research_Plan_Pediatric_Pulmonology.md).
- ✅ **Course reference slides** captured in the repo (see below).
- ⬜ **Interview guides** — per-stakeholder (physician, nurse, family, secretary) — not started.
- ⬜ **Interviews** — target 8–12, prioritising physicians & families — not started.
- ⬜ **Research Report** (graded, 40%) — due Thu 30 Jul — not started.

## What's in this repo

| File | What it is |
|---|---|
| `README.md` | This file — project overview and status. |
| `Research_Plan_Pediatric_Pulmonology.md` | The Research Plan (v1): problem, focus, research questions, methodology, participants, ethics, timeline, limitations. |
| `Research report - what we expect.jpg` | Course slide — the six things the graded report must do. |
| `Start now - desk research.jpg` | Course slide — desk-research guidance to feed the plan. |
| `Interviewing .jpg` | Course slide — do's & don'ts for hospital interviews. |
| `Timeline.jpg` | Course slide — the three-week sprint timeline. |
| `Deliverables and grading.jpg` | Course slide — what counts toward the grade. |

## Timetable

Sprint runs Fridays 08:45–13:00, plus team work in between.

| Date | Milestone | Notes |
|---|---|---|
| Fri 24 Jul | Kickoff + desk research begins | Plan drafted |
| **Sun 26 Jul** | **Research Plan due** (required, non-graded) | Submit `Research_Plan_...md` |
| Mon–Wed 27–29 Jul | Interviews + rolling synthesis | Physicians & families first |
| **Thu 30 Jul** | **Research Report due — 40% (graded)** | First graded deliverable |
| Fri 31 Jul | Research → ideation | Carry evidence into the concept |
| Thu 6 Aug | Initial Solution Concept — 10% | |
| Sun 9 Aug | Low-Fidelity Prototype (required) | |
| Thu 13 Aug | High-Fidelity Prototype + Fabrication (required) | |
| Fri 14 Aug | Presentation + Prototype Demo — 40% · Shared Skill due | |
| Sun 16 Aug | Contribution & Reflection — 10% (individual) | |

> **Date note:** the course deck lists the graded Research Report as **Thu 30 Jul** (not Friday). Confirm with the team before locking the schedule.

## Grading at a glance

- **40%** — Final Research Report (team) · Thu 30 Jul
- **10%** — Initial Solution Concept (team) · Thu 6 Aug
- **40%** — Presentation + Prototype Demo (team) · Fri 14 Aug
- **10%** — Contribution & Reflection (individual) · Sun 16 Aug
- Also required (non-graded): Research Plan, Low-Fi Prototype, Hi-Fi Prototype + Fabrication, and one reusable **Shared Skill** per team.

## Next steps

1. Push local commits to GitHub (`git push origin main`).
2. Draft per-stakeholder interview guides.
3. Confirm interview access through the partner hospital; schedule physicians & families first.
4. Run interviews, map the pre-visit intake journey, cluster themes.
5. Write the Research Report from the evidence (problem → method → findings → "so what" → limitations).

## For contributors (and their AI assistants)

If you're picking this up — human or AI — start here:

- **The one-line frame:** we're improving how a child's clinical history is collected *before* a pediatric pulmonology visit, so the physician isn't reconstructing it from scratch at the point of care.
- **Read first:** `Research_Plan_Pediatric_Pulmonology.md` is the source of truth for scope, research questions, and method. Don't broaden scope beyond pre-visit intake without a team decision.
- **Grounding rule:** claims in our deliverables must be backed by evidence (desk research or interviews) — "grounded in real evidence, not opinion." Back each theme with at least two independent sources before treating it as a finding.
- **Sensitivity:** pediatric hospital context. Never collect or store identifiable patient data; get consent; never record without permission. See `Interviewing .jpg`.
- **Conventions:** deliverables are Markdown in this repo so they diff and render on GitHub. Keep this README's status section current as work lands.

_Last updated: 24 July 2026._
