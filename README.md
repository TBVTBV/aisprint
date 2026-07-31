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

## Tasks & responsibilities

Each member holds one **lead role** for the whole sprint and also runs interviews (in pairs — one leads, one takes notes). Owners are a proposed split — adjust at kickoff, and put recruitment on whoever has the partner-hospital contact.

| Member | Lead role |
|---|---|
| **Matan** | Report & repo lead — owns the document, Git, submissions; books the mentor review |
| **Anat** | Recruitment & hospital liaison — single point of contact for scheduling |
| **Gal** | Field & synthesis lead — owns interview guides, journey map, theme clustering |
| **Mikhail** | Desk research & competitive-scan lead — keeps the evidence base current |

### The week, task by task

**Matan — Report & repo lead**

- [ ] Fri 24: push commits; keep repo + README current
- [ ] Sat–Sun: finalise & **submit the Research Plan**; book + run the mentor review
- [ ] Mon 27: physician interviews (notetaker); set up the Research Report skeleton
- [ ] Tue 28: family interviews (notetaker)
- [ ] Wed 29: co-lead synthesis with Gal; start drafting the report
- [ ] Thu 30: **assemble & submit the Research Report (40%)**
- [ ] Fri 31: carry evidence into ideation

**Anat — Recruitment & hospital liaison**

- [ ] Fri–Sat: contact the partner hospital; send the recruitment message; line up physicians, nurses, families, secretaries for Mon–Wed
- [ ] Sun 26: confirm the full week's interview schedule
- [ ] Mon 27: hold the schedule together; help Gal finalise the family guide
- [ ] Tue 28: **lead family/caregiver interviews**
- [ ] Wed 29: secretary/admin interviews (notetaker); feed notes into synthesis
- [ ] Thu 30: supply family quotes + notes to the report
- [ ] Fri 31: ideation

**Gal — Field & synthesis lead**

- [ ] Fri 24: set up & run **Claude Code in PowerShell** — install Node.js, then `npm install -g @anthropic-ai/claude-code`, then run `claude` inside the repo folder. Use it to draft guides and work the repo with AI assistance.
- [ ] Fri–Sun: draft the master interview-guide structure + the **physician and nurse guides**
- [ ] Mon 27: **lead physician interviews**
- [ ] Tue 28: **lead nurse interviews**; begin the pre-visit journey map
- [ ] Wed 29: **lead synthesis** — affinity-cluster themes, finish the journey map
- [ ] Thu 30: write the findings section of the report
- [ ] Fri 31: lead ideation off the evidence

**Mikhail — Desk research & competitive-scan lead**

- [ ] Fri–Sun: finish desk research + competitive scan; write up the evidence base; draft the **secretary/admin guide**
- [ ] Mon 27: continue desk research; keep sources current
- [ ] Tue 28: nurse interviews (notetaker)
- [ ] Wed 29: **lead secretary/admin interviews**
- [ ] Thu 30: supply the background + landscape section to the report
- [ ] Fri 31: ideation

### Interview pairings

Physicians — Gal leads, Matan notes · Nurses — Gal leads, Mikhail notes · Families — Anat leads, Matan notes · Secretaries/admin — Mikhail leads, Anat notes.

## Current status — as of 24 July 2026

- ✅ **Challenge selected and scoped** to pre-visit intake (vs. point-of-care capture or the whole journey).
- ✅ **Desk research done** — documentation/history-taking burden, existing tools (c-ACT), environmental-trigger under-reporting, proxy-report limitations. Findings feed the Research Plan background.
- ✅ **Research Plan drafted (v3) & committed** — meets the sprint "done" checklist (owners assigned, mentor review pending). See [the Research Plan in Drive](https://docs.google.com/document/d/1GGYgcYeDJR3qa4hW9B2Hy7i2mjBLLjJzYw0xZJxSBIg/edit); also mirrored as an editable Google Doc in the team Drive.
- ✅ **Team knowledge base set up in Google Drive** — a shared hub with Deliverables / Interviews / Synthesis / Course-materials folders (see "Where we work" below). The course reference slides now live in the Drive Course-materials folder, not this repo.
- ⬜ **Interview guides** — per-stakeholder (physician, nurse, family, secretary) — not started.
- ⬜ **Interviews** — target 8–12, prioritising physicians & families — not started.
- ⬜ **Research Report** (graded, 40%) — due Thu 30 Jul — not started.
- ✅ **Shared Skill consolidated** — four teammates each built one skill independently; three were about interview material and were merged into a single `interview-synth` with Generate / Synthesize / Panel modes. See [`skills/README.md`](./skills/README.md) for the comparison and [the process write-up in Drive](https://drive.google.com/file/d/16G9LYp4iZOFRkYCBIpNPH78EoC3Ut0ji/view) for the write-up.

## Where we work

Two places, on purpose:

- **Google Drive — the team knowledge base** (open [📌 START HERE — Group 7 Research Hub](https://docs.google.com/document/d/1Znx_i4E5HxupoteUlM2AHywBgT8IX-_vlnyBeR09Fgo/edit)). All collaborative work lives here so everyone can edit without GitHub: the Research Plan as a Google Doc, interview notes (Interviews folder), synthesis and journey map (Synthesis folder), and the course slides (Course materials folder).
- **GitHub — this repo** — version-controlled deliverables (Markdown) and the required reusable **Shared Skill** for the coders.

## What's in this repo

The repo is deliberately narrow: **skills, plus the product and prototype we are about to build**. Written deliverables (the Research Plan, the Research Report, the Shared Skill process write-up) live in the Google Drive hub, not here.

| File | What it is |
|---|---|
| `README.md` | This file — project overview, status, and the team's map. |
| `skills/interview-synth/` | The team's reusable **Shared Skill**, consolidated. One skill, three modes: **Generate** a grounded, clearly-labelled synthetic interview; **Synthesize** transcripts into an evidence-weighted findings report; **Panel** an idea against the stakeholders we interviewed. All three sit on one evidence ladder and one guardrail set (grounding, permanent labelling, no identifiable patient data, provenance). Includes `references/background.md` and a full worked example under `assets/`. |
| `skills/README.md` | How the four team-member skills compared and why they were merged into one. |
| `.claude/skills/` | Where Claude Code auto-discovers skills. Holds `progress-tracking` (Drive vs plan audit) and a symlink to the consolidated `interview-synth`. |

_The course reference slides and the editable plan now live in the Google Drive hub (see "Where we work")._

## Timetable

Sprint runs Fridays 08:45–13:00, plus team work in between.

| Date | Milestone | Notes |
|---|---|---|
| Fri 24 Jul | Kickoff + desk research begins | Plan drafted |
| **Sun 26 Jul** | **Research Plan due** (required, non-graded) | Submitted (see Drive) |
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
- **Where the work lives:** the **Google Drive hub** (see "Where we work") is the day-to-day knowledge base — interview notes, synthesis, and the editable plan. This **repo** holds the version-controlled Markdown deliverables and the Shared Skill. Read [the Research Plan](https://docs.google.com/document/d/1GGYgcYeDJR3qa4hW9B2Hy7i2mjBLLjJzYw0xZJxSBIg/edit) first — it's the source of truth for scope, research questions, and method. Don't broaden scope beyond pre-visit intake without a team decision.
- **Grounding rule:** claims in our deliverables must be backed by evidence (desk research or interviews) — "grounded in real evidence, not opinion." Back each theme with at least two independent sources before treating it as a finding.
- **Sensitivity:** pediatric hospital context. Never collect or store identifiable patient data; get consent; never record without permission.
- **Conventions:** the repo holds skills and, from here on, the product and prototype code; written deliverables and collaborative editing live in the Drive Google Docs. Keep this README's status section and the Drive hub current as work lands.

_Last updated: 31 July 2026._
