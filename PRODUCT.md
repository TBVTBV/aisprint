# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack

static HTML/CSS/JS, self-contained single files. No build step, no CDN, no network at runtime, no browser storage. Each deliverable is one `.html` file that opens by double-click from a Google Drive folder synced to a laptop.

## Users

Four HCI master's students on Group 7 of the AI Product Sprint 2026 at Reichman University: Matan Rosen (report and repo lead), Anat Katzir (recruitment and hospital liaison), Gal Yeshayahu (field and synthesis lead), Mikhail Yagudaev (desk research and competitive scan). They open these pages on laptops between 31 July and 6 August, working toward the Initial Solution Concept, rearranging clusters and referring back to evidence.

Secondary and decisive for the design: two pediatric pulmonologists who are also the team's mentors (Dr. Patrick Stafler, Dr. Ophir Bar-On, Schneider Children's) and the course staff, who open the pages with nobody there to explain them. Every claim must carry its source on the surface.

## Product Purpose

Turn one week of pediatric-pulmonology field research into a point of view and a set of testable solution directions, in a form a team can work in and a mentor can audit unaccompanied. Success is a mentor being able to trace any statement back to the interview it came from, and the team being able to rearrange the evidence without losing that traceability.

## Positioning

The two things that make this different from a generic research board: every observation carries the interview it came from and whether it counts as evidence, and synthetic material is separated from real material at the level of the individual note rather than in a footnote. A neighboring research tool shows themes; this one shows what each theme rests on, and lets you subtract the synthetic half and watch whether the theme survives.

## Operating Context

Challenge #6, pediatric pulmonology, scoped to pre-visit intake: how a child's clinical history is collected before the appointment and why it reaches the physician incomplete.

Team knowledge base is a shared Google Drive folder (Deliverables / Interviews / Synthesis / Course materials) with a GitHub repo alongside for skills and code. These two pages live in the Synthesis folder next to `Group7_S2_Synthesis.docx` and `Group7_S2_Ideation.docx`, which carry the identical content.

Course rituals that bear on the work: Session 2 (31 July) runs synthesize then ideate as one timed block; the Initial Solution Concept is due 6 August; mentor reviews happen by email and WhatsApp between sessions.

## Capabilities and Constraints

- Two artifacts. One covers synthesis (affinity map, two personas, two journey maps, five insights, POV, three How Might We). One covers ideation (22 concepts, three converged directions with riskiest assumption and smallest test).
- Content is fixed and must match the .docx versions verbatim. The HTML is a different rendering of the same evidence, not a rewrite.
- Course templates the personas and journey maps must follow: "AI Product Sprint 2026 - Persona Template" and "AI Product Sprint 2026 - Journey Map Template".
- No browser storage of any kind. A rearranged board is exported as a downloaded JSON file or it is not kept.
- Pages must work offline, opened from a local file path.

## Brand Commitments

None binding. The course deck's own presentation is not a constraint on these artifacts.

## Evidence on Hand

Real participants, six interviews:

- Dr. Patrick Stafler and Dr. Ophir Bar-On, pediatric pulmonologists, Schneider Children's, 26 Jul. Transcript, summary, quote bank of 20 numbered quotes.
- Pediatric pulmonologist, Clalit hospital clinic, 30 Jul. Hebrew transcript plus English debrief.
- Pediatric pulmonologist, hemato-oncology focus, Pulmonary Institute Schneider, 30 Jul. English debrief.
- Two pediatric pulmonology intake/triage nurses, 29 Jul. One Hebrew transcript, one English transcript.

Desk research and competitive scan, v5, 29 Jul, with numbered citations (Overhage & McCallie 2020; Weiss et al. CAMP 2001; Liu et al. c-ACT 2007; PedsQL proxy-agreement studies; Ofek/Eitan health-information-exchange literature).

Three LLM-generated family/caregiver interviews, each labelled SYNTHETIC in its own header, footer and quote bank. **No real family or caregiver was interviewed.** This absence must never be papered over: synthetic material is excluded from participant counts and from the weight of any finding, and future work must not present it as evidence or invent real families to replace it.

Not on hand and not to be invented: verified in-room timings (the fifteen-minute-to-one-hour figure is unverified against the recording), any real family quote, any figure for this clinic's own throughput beyond what participants estimated aloud.

## Product Principles

1. **Provenance travels with the claim.** Every observation shows its source and its weight at the point of use, not in an appendix. A mentor must never have to ask where a line came from.
2. **Synthetic is visible at note level.** Real and synthetic never share a visual treatment. The reader can remove the synthetic material and see what survives.
3. **The board is a working surface, not a diagram of one.** If the method says one observation per note and clusters formed bottom-up, the artifact has to actually be made of movable notes.
4. **Evidence over assertion.** A theme is a finding only where at least two independent real sources support it, and the artifact shows the count.
5. **No identifiable patient data, anywhere, ever.** Pediatric hospital context. This is a gate, not a preference.

## Accessibility & Inclusion

Colour never carries meaning alone; every source-coded element carries a text label. Categorical palette validated for colour-vision deficiency in both light and dark. Full keyboard path for every interaction including moving a note between clusters. Respects `prefers-reduced-motion` and `prefers-color-scheme`. Hebrew source quotes appear in translation with the original preserved where the quote bank holds it.
