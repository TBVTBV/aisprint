# CLAUDE.md — Group 7, AI Product Sprint 2026

Context for Claude Code working in this repo. Read `README.md` for the project overview and `PRODUCT.md` for durable product truth. This file covers what is in flight and how to finish it.

---

## The one-line frame

We are improving how a child's clinical history is collected **before** a pediatric pulmonology visit, so the physician is not reconstructing it from scratch at the point of care. Challenge #6. HCI Master's, Reichman University.

**Team:** Matan Rosen (report & repo), Anat Katzir (recruitment & hospital liaison), Gal Yeshayahu (field & synthesis), Mikhail Yagudaev (desk research & competitive scan).

---

## Where the work lives

| | |
|---|---|
| **Google Drive** (the knowledge base) | `~/Library/CloudStorage/GoogleDrive-mr.matan.rosen@gmail.com/.shortcut-targets-by-id/1JWMNO1HXta6rOKVPGaXJpu6NQUALRYJF/Group 7 - Gal, Anat, Mikhail, Yarden, Matan/` with `Deliverables/`, `Interviews/`, `Synthesis/`, `Course materials/`, `Reviews/` |
| **This repo** | Skills, and from here on the product and prototype code |
| **Session 2 deliverables** | `Synthesis/Group7_S2_Synthesis.docx` and `Synthesis/Group7_S2_Ideation.docx`, both final |

Interview transcripts, debriefs and quote banks are in Drive `Interviews/`. Never copy identifiable patient data into this repo, and never quote a synthetic interview as though it were real.

---

## Evidence base, and the rule that governs it

**Six real interviews.** Four pediatric pulmonologists (Stafler & Bar-On at Schneider 26 Jul; a Clalit hospital clinic physician 30 Jul; a hemato-oncology-focused pulmonologist at Schneider 30 Jul) and two pulmonology intake nurses (29 Jul). Plus a desk research and competitive scan, v5.

**Three synthetic caregiver interviews.** LLM-generated. **No real family or caregiver was interviewed.** They are excluded from participant counts and from the weight of any finding, they are labelled at every point of use, and they are a device for stress-testing clinician-reported claims, never a finding.

**Grounding rule.** A point becomes a finding only where at least two independent *real* sources support it. If you write a claim, put its source next to it.

**Hard gate.** No identifiable patient data enters an AI model, ever. A physician told us they do it anyway "in a pirate way" and named that as a problem. Any concept requiring it is disqualified, not merely risky.

---

## What Session 2 produced (31 Jul)

Four artifacts, identical content, two formats.

| File | State |
|---|---|
| `Group7_S2_Synthesis.docx` | **Done.** In Drive `Synthesis/`. Affinity map (6 clusters, 45 observations), two personas on the course template, two journey maps on the course template, five insights, one POV, three HMW, guardrails. |
| `Group7_S2_Ideation.docx` | **Done.** In Drive `Synthesis/`. The bundle, 22 concepts, three converged directions with riskiest assumption and smallest test, recommendation. |
| `Group7_S2_Synthesis.html` | **Draft, working, not finished.** See below. |
| `Group7_S2_Ideation.html` | **Draft, working, not finished.** See below. |

### The five insights, in short

- **I1** Physicians are not short of information, they are short of a route to it. Design target is retrieval latency and click-depth, not comprehension.
- **I2** Verification is not overhead on the visit, it is the visit. Any system that hands a physician a conclusion is rejected even when correct. Automate only where there is no judgement (normality flagging), accelerate everywhere else. **This kills "AI summarises the chart".**
- **I3** The holes in the record sit on organisational boundaries, which makes them predictable per patient from the referral alone.
- **I4** The family failure is instructional and reciprocal, not motivational. An ask nobody owns, and an ask that is not visibly used, decays. The clinic's own checklist already died this way.
- **I5** Asking families for more produces more confident answers, not truer ones. Intake must carry its own uncertainty and make "I don't know" a recorded value.

### POV

> A pediatric pulmonologist facing a new patient needs to reach and verify the raw pieces of that child's history faster, not to be handed a summary, because the visit is consumed by re-assembling a record that is fragmented exactly where one organisation ends and the next begins, and that, in their own words, is never complete.

### The three directions

- **A · One Route, No Conclusions** (recommended primary). Pre-fetched, rubric-organised view, every item one click from the raw artefact, nothing summarised. Riskiest assumption: physicians use it instead of falling back to the systems they trust. Smallest test: paper mock, one de-identified case, three physicians, count every reach past the mock.
- **B · The Named Ask.** A short, specifically-named pre-visit list derived from what the record could not reach, with a safe "I don't know". Riskiest assumption: the named ask gets completed where the generic one did not, and the answers are accurate enough to change what the physician does. Smallest test: concierge, five families, phone call two days out.
- **C · Nothing Arrives Without an Owner.** Expected-artefacts checklist per upcoming chart with a named owner. Riskiest assumption: the loss is visibility, not capacity. Smallest test: one clinic day, done by hand.

---

## The two HTML artifacts, and how to finish them

Both are single self-contained files: inline CSS and JS, no CDN, no network, no browser storage, open by double-click. They pass the impeccable detector clean and pass a 22-assertion Playwright interaction suite. **They failed the finish review.** The findings below are unapplied. Work the list top down.

### Design direction contract

Both files carry a `DIRECTION CONTRACT` comment as the first child of `<body>`. Do not delete it, and audit the render against it when you change anything.

- **Seed key `db4ae67f`**, mode `operate`, assigned index 5.
- **World:** a pen-plotter instrument trace on graph paper. Continuous 40px grid with 200px majors, regions bounded by hairline rules and channel baselines rather than shadowed cards, warm paper `#f7f6f1`, graphite ink `#14140f`, 2px radius, wide-tracked uppercase instrument labels, tabular figures.
- **Thesis:** provenance is the visual system. Every observation shows its source and weight where it sits, and the synthetic half can be subtracted to see what survives.

### Palette

Source hues are CVD-validated in both modes with the dataviz validator. The **light values below are the corrected, text-safe steps** computed but not yet applied. Applying them is finding 1.

| Role | Light (apply this) | Light (current, failing) | Dark (fine) |
|---|---|---|---|
| Physician | `#1d5fae` (6.24:1) | `#2a78d6` (4.33:1) | `#3987e5` |
| Nurse | `#0d7a52` (5.25:1) | `#1baf7a` (2.76:1) | `#199e70` |
| Synthetic | `#b84714` (5.22:1) | `#eb6834` (3.14:1) | `#d95926` |
| Desk research | neutral `#5d5a53` + 45° hatch | same | `#9d9a90` |

The new light triple re-validates: CVD all-pairs PASS, normal-vision floor 18.8, contrast PASS.

### Open findings, ranked

1. **The SYNTHETIC label is the lowest-contrast text on the page in light mode** (3.14:1). It is the label that carries the project's central honesty claim. Swap in the text-safe light hues above.
2. **`Group7_S2_Ideation.html` `.card[data-dim="true"]{opacity:.22}` destroys the page's own thesis.** De-selected concepts drop to ~1.5:1, so "what was left behind is visible" becomes false. Encode the state on the surface, not the ink: `background:var(--sunk)`, `border-top-color:var(--rule-soft)`, body text to `--ink-3`. No opacity below 0.6 anywhere.
3. **Direction B's prose list omits concept 22, Pre-Visit Concierge, which the interaction does light.** Concept 22 *is* B's smallest test. Generate the `concepts` string from the `CONCEPTS` array so it cannot drift, and order C's list.
4. **`Group7_S2_Synthesis.html` masthead "Synthetic, excluded · 3" is false as rendered.** There are 4 synthetic notes, on by default, inside the 45. Change to "Observations, real 41 / Observations, synthetic 4" and amend the section intro to say the synthetic notes are present and labelled.
5. **The five insights are collapsed with no disclosure affordance,** and the source count renders as `●●●○` with the number nowhere in text. Add an Open/Close affordance, open I1 by default, print "3 real sources" as text.
6. **The keyboard path for moving a note ends by throwing focus to `<body>`,** because `renderBoard()` destroys the element `lastFocus` points at. Re-focus the moved note by id. Separately the drawer is modal in behaviour but `aria-modal="false"` with no focus trap: pick one modality and commit.
7. **Every rail link hides the section it navigates to** under the sticky rail. `main section[id]{scroll-margin-top:58px}`.
8. **A kicker above every heading.** The craft floor bans this outright, and the instrument-label device is being used as its alibi. Delete the eyebrow above the h1, above all seven section h2s, above the persona h3s and above each direction h3. Fold "Direction A" into its own heading. Keep the numbering in the rail only. Also drop the decorative 1/2/3 from the three lean-lens columns, which are parallel, not sequential.
9. **The affinity board side-scrolls between 960px and 1488px,** which is most laptops. Add breakpoint bands: 3 columns under 1500px, 2 under 1080px, 1 under 960px.
10. **`Group7_S2_Ideation.html` has no empty state.** Toggle all four tag chips off and the grid is blank. The synthesis board already has the right vocabulary per column.
11. **`<q>` is applied to desk-research paraphrases,** which renders published studies as though they said those words verbatim. Add a `kind` field and only wrap real quotes. Two notes also double up quote marks: switch their inner literals to single curly quotes.
12. **Hebrew originals and translation marking are absent,** against `PRODUCT.md`'s accessibility section. Four of the six real interviews were conducted in Hebrew. Add `lang` and `original` to the note model and mark translated notes on the slip and in the drawer.
13. **The journey feeling scale is unreadable as data.** Four levels exist, only two are labelled on the axis, no stage carries its feeling as text, and the SVG `aria-label` reads glyph names aloud. In overlay mode the two lanes differ by hue alone. Label all four levels, add the feeling word to each stage header, clean the aria label, and give the caregiver lane a dashed stroke and a distinct marker.
14. **The "held back" badge is a hyphen in `--ink-4` inside a dashed box** and reads as an empty checkbox. Seven of 22 concepts are marked this way with no key. Use a readable text badge and add a one-line key beside the direction buttons.
15. **Filter chips encode "off" as `opacity:.5`.** Express it with border and surface, keep text at full contrast.

Minor, worth a sweep: no skip link; `contenteditable` cluster names have no affordance; three button vocabularies in the ideation file; the rail's hidden scrollbar gives no cue on mobile; the theme toggle announces as "Light, pressed"; dead code (`.ins .more` styled but never rendered, an `IntersectionObserver` constructed and never observed at the end of the ideation script); the persona Context facet leaves ~40% of its row empty; `.land` is a default card triptych.

### Verify loop

```bash
# mechanical scan, must return []
node .claude/skills/impeccable/scripts/detect.mjs --json Group7_S2_Synthesis.html Group7_S2_Ideation.html

# interaction suite, 22 assertions (needs python playwright)
python3 test.py
```

Render and actually look at the output before calling anything done. Crop tall screenshots into slices; a full-page thumbnail hides exactly the failures that matter.

---

## Working agreements

- **Evidence, not opinion.** Two independent real sources before a theme becomes a finding.
- **Synthetic is visible at note level.** Real and synthetic never share a visual treatment.
- **No identifiable patient data.** Anywhere, ever.
- **Provenance travels with the claim.** A mentor must never have to ask where a line came from.
- **Anything we propose names an owner and a measurement,** or it decays the way the clinic's last checklist did.
- Do not broaden scope beyond pre-visit intake without a team decision.

## Tooling notes

- `impeccable` is vendored at `.claude/skills/impeccable/`. It requires `PRODUCT.md`, which is in this repo. The direction roll (`concept-seed.mjs`) ran degraded with no network, so there were no challengers and no quality-bar boards. If you re-roll with network available, use `--from db4ae67f` to stay consistent.
- The finish review that produced the list above was run by a substituted general-purpose reviewer, not the shipped `impeccable-finish-reviewer`, because that agent was unavailable in that environment. Re-run the real one if you have it.
- `DESIGN.md` has not been written. Per the impeccable flow it is written at finish, from the built world. Write it once the findings above are closed.

## Calendar

Initial Solution Concept, 10%, **Thu 6 Aug**, built off Direction A. Low-fi prototype Sun 9 Aug. Hi-fi + fabrication Thu 13 Aug. Presentation + demo, 40%, and the Shared Skill, Fri 14 Aug. Contribution & reflection, 10%, Sun 16 Aug.

Before Session 3: book the three physician mock sessions and five family calls through the mentors, **interview real families** (every family-side claim is currently synthetic), verify the fifteen-minute-to-one-hour in-room figure against the recording, and write the Initial Solution Concept off Direction A.
