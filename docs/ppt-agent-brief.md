# Brief: building a PowerPoint for this project

Standing instructions for an agent asked to produce a presentation (share-out, mentor
review, final demo) about **Beforehand**, Group 7's pre-visit intake prototype. Read this
whole file before opening PowerPoint tooling. Use the `pptx` skill to author the file.

## Context you must carry

- **Course:** AI Product Sprint 2026, HCI Master's, Reichman University. Group 7:
  Matan Rosen, Anat Katzir, Gal Yeshayahu, Mikhail Yagudaev.
- **Challenge #6:** pediatric pulmonology — a child's clinical history reaches the
  physician incomplete, fragmented exactly where one organisation ends and the next
  begins. Scoped to **pre-visit intake**, the caregiver side.
- **Evidence base:** six real interviews (four pediatric pulmonologists, two intake
  nurses) plus desk research. Three caregiver interviews are **LLM-generated synthetic**
  material: they are labelled, excluded from participant counts, and must never be
  presented as evidence. **No real family has been interviewed** — never paper over this.
- **The product:** Direction B, "The Named Ask". A phone-first, self-contained web app a
  caregiver opens from the clinic's SMS. It is rendered as a **chat with the clinic**
  ("WhatsApp, but blue"): a splash, a faked phone+OTP gate, an accumulating conversation
  of 6–9 branching questions, a named list of 3–5 specific documents only the family can
  supply, review-by-conversation, and a single שלח send. "I don't know" is a first-class
  answer; machine-read documents are flagged and correctable; partial completion is a
  success state; nothing is real PII (the child "Yotam", "Dr. Oren Segev" and clinic
  "Gordon" are all fictional and every deck must say so).
- **What the prototype is for:** it is the *stimulus* for concierge calls with real
  families and the artifact for share-outs — not the test itself.
- Authoritative sources, in order: `PRD.md` (product truth and copy),
  `previsit-design.md` (visual world and its history), `CLAUDE.md` (evidence rules),
  `README.md` (links). Quote copy from the PRD verbatim; do not invent claims, numbers,
  or research findings.

## Design system for slides

Slides must look like the product. Palette:

- Deep blue `#24518F` (headers, title slide background), action blue `#2D5FA8`
  (accents, highlights), tint `#E7EEFB` (panels), caregiver-bubble blue `#D5E3F8`,
  wallpaper `#E9EEF5` (light slide backgrounds), ink `#20242A`, muted `#6A7385`.
- **No red anywhere.** Amber `#8A6415` is the only attention color, used sparingly.
- Type: a clean geometric sans (Rubik if available, else Calibri/Arial). Hebrew slides
  are RTL: right-align Hebrew text, set paragraph direction RTL, keep numerals and Latin
  product names LTR inline.
- Shapes: rounded corners (12–16px feel), pill-shaped buttons in mockups, one soft
  shadow at most. Generous white space. No clip-art, no stock photos, no gradients.
- Illustrations: use the project's hand-drawn set in `/illustrations` (blue ink +
  sky-blue circle accent). They have white backgrounds in source; place them on white
  slides, or strip the background as done in the app.
- Tone: calm and warm, not salesy. The deck should feel like the clinic speaking.

## Assets

- `docs/screens-before-redesign/` — 17 PNGs of the pre-redesign greyscale wireframe
  (numbered in flow order). Use for before/after comparisons.
- Current app screenshots: capture fresh from `previsit-intake.html` with Playwright at
  390×844, deviceScaleFactor 2, screenshotting the `#app` element; drive the flow via the
  `window.__app` debug hooks (see the capture scripts pattern in git history). The live
  URL is https://tbvtbv.github.io/aisprint/ once merged to `main`.
- Design exploration boards, if telling the design story: `design-explorations.html`
  (4 divergent directions), `design-chat-explorations.html` (4 chat variants),
  `design-chat-back-options.html` (6 back-navigation options),
  `design-chat-final.html` (the committed spec).
- The clinic logo lives as inline SVG in `previsit-intake.html` (search `logoSVG`).

## Default deck outline (adapt to the ask)

1. Title — Beforehand, team, challenge; fictional-data disclaimer in the footer.
2. The problem — 60–70% of a first visit spent reconstructing history; the caregiver got
   "bring whatever you have", which is uninterpretable. Two quotes max, sourced.
3. Evidence — 6 real interviews + desk research; synthetic material named as synthetic.
4. The insight that kills the obvious idea — verification *is* the visit; no AI summary.
5. Direction B: The Named Ask — specific documents, "I don't know" as data, reciprocity
   ("Dr. Oren reads this before you walk in").
6. The prototype as a conversation — 3–4 phone screenshots (splash → chat → documents →
   send). Show the tap-to-edit and the flagged machine-read moment.
7. Before/after — one wireframe PNG beside the same screen today.
8. What we're testing next — concierge calls with five real families; what would falsify
   the direction.
9. Ask/close — what we need from mentors.

## Hard rules

- Every claim traceable to `PRD.md`/`CLAUDE.md`; every quote attributed to its interview.
- Synthetic material always labelled at point of use; never in participant counts.
- Fictional-data notice appears at least once, visibly.
- No em dashes in slide copy. Hebrew decks: no letter-spacing, no all-caps styling.
- Keep it under ~10 content slides unless asked otherwise; one idea per slide.
