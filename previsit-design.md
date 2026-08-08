# previsit-design.md — Design direction for the pre-visit intake app

> The design contract for `previsit-intake.html`. The S2 research artifacts have their own
> world in `DESIGN.md`; this file owns the **app**. It follows the design.md conventions AI
> agents consume: product brief first, then tokens with usage rules, components with absolute
> values, and an explicit don'ts list.
>
> **Status: superseded by the committed chat world, now implemented.** After this document
> was written, the team explored four divergent directions (`design-explorations.html`),
> chose the conversational one, sharpened it over seven rounds (`design-chat-explorations.html`,
> `design-chat-back-options.html`), and froze the spec in **`design-chat-final.html`** —
> "WhatsApp, but blue." That world now ships in `previsit-intake.html` and is recorded in
> PRD §13. Sections 2 and 8–10 below still bind (principles, voice, accessibility, don'ts,
> minus the teal palette); sections 3–7 are the research-backed first direction, kept as
> the record of how the committed world was reached.
>
> **The committed world, in short:** deep-blue header `#24518F` with the Gordon clinic logo
> avatar and kebab menu; dotted wallpaper `#E9EEF5`; white clinic bubbles with the sharp
> corner toward the mini logo avatar, light-blue `#D5E3F8` caregiver bubbles with a generic
> person mark; quick-reply pills (selected = solid `#2D5FA8` with a check); an accumulating
> conversation where tapping an answer opens a focused edit mode; a textless continuous
> progress bar above skip/הבא; the solid-plane "שלח" only on the final screen. No red,
> anywhere, ever.

---

## 1. Product brief

A phone-first form a caregiver opens from an SMS link, two days before her child's first
pulmonology visit. She answers a handful of questions and photographs a few named documents
so the physician reads it all before she walks in. She is tired, holding an infant, probably
in WhatsApp's in-app browser, and worried about her kid. The UI's job is to make four minutes
of honest answering feel light, safe, and obviously worth it.

**Look target: approachable Israeli B2C**, closer to a well-made consumer app (Flo, Ada,
Headspace) than to a hospital portal. Calm, warm, rounded, generous — but quiet: this is a
clinic speaking, not a startup shouting.

## 2. Principles

1. **Calm over clinical.** Soft warm surfaces, no sterile white-and-blue, no alarm colors.
   Patients open health apps in stressful moments; the interface must lower the pulse, not
   raise it (Eleken: "calm visual language to build trust").
2. **One thing per screen, one hand.** A single question, a single primary action, pinned
   where a thumb already is. Ada's one-question-at-a-time pacing is the model.
3. **Honesty is styled, never hidden.** "I don't know", skips, and the machine-read
   uncertainty flag get real visual respect — tinted, labeled, first-class. Never red,
   never shame (PRD guardrail 12.5 carries into the visual layer).
4. **Progress is felt.** Rounded segments filling, gentle transitions, quick wins early.
   Completion should feel like the app saying "thank you", not "finally".
5. **Hebrew is the design language.** RTL is the default composition, Latin is the guest.
   Type, alignment, and iconography are chosen for Hebrew first.

## 3. Color tokens

Warm neutrals + one calm teal. Teal reads "health" without hospital-blue chill and without
Clalit/Maccabi brand collision. All text pairings must re-validate ≥4.5:1 at implementation
(run the dataviz validator; values below are chosen to pass but verify).

| Token | Value | Role and rules |
|---|---|---|
| `--ground` | `#F7F4EF` | Page ground outside the phone frame; warm paper |
| `--surface` | `#FFFFFF` | Cards, sheets, bars |
| `--surface-2` | `#F1EDE6` | Sunken/secondary surfaces: pressed states, disabled fills, DX slot |
| `--ink` | `#24292E` | Primary text. Warm near-black, never pure #000 |
| `--ink-2` | `#5B6168` | Secondary text, hints, meta lines |
| `--primary` | `#0E6F63` | The one brand color. Primary buttons, progress fill, links, selected states |
| `--primary-ink` | `#FFFFFF` | Text on primary |
| `--primary-tint` | `#E3F1EE` | Selected option fill, chips-on, info surfaces. Never for text |
| `--attention` | `#9A5B00` | The uncertainty color: flagged read fields, "can't get" states. Amber, not red |
| `--attention-tint` | `#FBF1E2` | Surface behind attention content |
| `--positive` | `#2F6B45` | Sent/success confirmations only, sparingly |
| `--line` | `#DED8CE` | Hairlines, borders, dividers |

Rules: exactly one saturated hue per screen (the primary); attention appears only where
uncertainty genuinely exists; **red exists nowhere in the palette** — there is no error
state worth frightening a parent for (PRD 12.5, 17). Color is never the only carrier of
state (icon or text always accompanies it).

## 4. Typography

- **Face:** Rubik — Hebrew+Latin harmonized, gently rounded terminals, the de-facto
  approachable Israeli B2C voice. Self-containment rule (PRD §14, no CDN/network) means:
  embed a subsetted woff2 (Hebrew + Latin + digits, weights 400/600) as data URIs, or fall
  back to the system stack. Decide by file-size budget at implementation; the fallback stack
  is `system-ui, -apple-system, "Segoe UI", Roboto, sans-serif` and must remain last in the
  stack either way.
- **Scale (px):** screen title 22/600 · question text 19/600 · option & body 16/400 ·
  meta/hints 13/400 · section labels 13/600. Line-height 1.5 body, 1.3 titles.
- **Numbers:** `font-variant-numeric: tabular-nums` on counts, dates, progress.
- **Hebrew rules:** no letter-spacing, no all-caps effects, no justified text; start-aligned
  everywhere. Latin in Hebrew sentences (drug names) stays LTR via `<bdo>`/`dir=ltr` spans.

## 5. Shape, space, elevation

- **Radius:** cards and sheets 16px · buttons 14px · chips and pills full-round · inputs 12px.
  Nothing square-cornered survives.
- **Spacing:** 4px base. Screen padding 20px. Card padding 16px. Stack gap between options 10px.
- **Touch:** every target ≥44×44px. Options are full-width rows, min-height 52px.
- **Elevation:** one soft shadow only — `0 1px 3px rgba(36,41,46,.08)` on cards and the
  bottom bar; sheets get `0 -4px 24px rgba(36,41,46,.12)`. No stacked shadows, no glows.

## 6. Components

- **Primary button:** full-width, 52px, `--primary` fill, white 16/600 text, radius 14px.
  Pressed: darken 8%. Disabled: `--surface-2` fill + `--ink-2` text, never transparent.
  One per screen, always in the sticky bottom bar on flow screens.
- **Secondary button:** `--primary-tint` fill, `--primary` text. No grey-bordered ghosts.
- **Text button:** `--primary` text, no underline at rest, underline on press/focus.
- **Option row:** `--surface` fill, 1px `--line` border, radius 14px. Selected:
  `--primary-tint` fill, 2px `--primary` border, leading check. "I don't know" renders
  identically to other options — same size, same weight (PRD 7.4).
- **Chips (confidence, date shortcuts, filters):** pill, 36px, tint-fill when on.
- **Document card:** surface card, 16px radius; a small line-icon block (paper/video) top,
  title 16/600, meta 13, the "why" line as a `--primary-tint` aside. Status replaces actions
  with a tinted band: teal for attached, amber for can't-get, neutral for will-bring/later.
- **Progress:** rounded 6px segments, `--primary` fill, animated width 200ms. Count line 13px.
- **Sheets (menu, privacy, explain):** bottom sheets with 16px top radius and a drag-handle
  bar, scrim `rgba(36,41,46,.4)`.
- **Loaders (checking / reading / sending / language):** calm text + three-dot pulse.
  No spinners, no skeletons — waits here are 1–1.5s theater (PRD §10) and should feel human.
- **The flagged read field:** `--attention-tint` background, `--attention` 13px label
  "We're not sure we read this correctly", edit affordance visible. This moment is the
  product's honesty on display — style it proudly, not as an error.

## 7. Motion

150–220ms, ease-out, translate ≤8px. Screen changes: content fades/slides 8px. Inline
reveals: height+fade in 200ms. Progress fill animates. Selected option: 120ms tint fill.
`prefers-reduced-motion: reduce` collapses all of it to instant. Motion never blocks input.

## 8. Voice

Already established and non-negotiable (PRD 7.1): full sentences addressed to the caregiver,
warm and concrete, zero guilt, zero clinical distance, "I don't know" treated as useful.
The visual system must match the writing — a rounded, warm UI wrapping cold telegraphic
copy, or vice versa, breaks the spell. Both locales always; Hebrew first.

## 9. Accessibility floor (unchanged from PRD §14)

Text ≥4.5:1 on its surface. Visible 2px focus rings (`--primary`) on controls — headings
excluded. Keyboard path through every screen. Real labels, `aria-live` on progress and
loaders, `aria-expanded`/`aria-pressed` where state exists. RTL structural. 44px targets.

## 10. Don'ts

- Don't use red, anywhere, for anything.
- Don't put two primary buttons on one screen, and don't stack more than two CTAs.
- Don't use photography, stock imagery, or emoji as icons; only the inline line-icon set.
- Don't add letter-spacing or caps styling to Hebrew text.
- Don't use grey "ghost" buttons for secondary actions — tint them.
- Don't animate anything longer than 250ms or move anything further than 8px.
- Don't use spinners or skeleton screens; the loaders are calm text moments.
- Don't style "I don't know" or Skip as lesser choices (smaller, greyer, tucked away).
- Don't let the attention amber appear on a screen where nothing is genuinely uncertain.
- Don't introduce a second saturated hue; illustrations, if added, use the existing palette.
- Don't break self-containment: no CDN fonts, no icon fonts, no external anything (PRD §14).

## 11. Open questions for the team

1. **Spot illustration** — a small warm line-illustration on landing/sent (paper, phone,
   checkmark) in the Headspace direction: adds approachability, costs bytes and taste risk.
   Recommend: yes, two spots max, single-color line style in `--primary`.
2. **Rubik embedded vs system stack** — ~120–180KB added for two subsetted weights.
   Recommend: embed; the face carries most of the B2C warmth on Android.
3. **Dark mode** — skip for P0 (demo runs in daylight, in-app browsers), revisit post-sprint.

## Sources

- [Eleken — Healthcare UI design best practices + examples](https://www.eleken.co/blog-posts/user-interface-design-for-healthcare-applications)
- [Merge — 8 best designed health apps](https://merge.rocks/blog/8-best-designed-health-apps-weve-seen-so-far)
- [Design Monks (Medium) — Healthtech UX in 2025](https://designmonks.medium.com/healthtech-ux-in-2025-best-practices-for-patient-monitoring-ui-ux-design-services-7a3763d1e63d)
- [Excellent WebWorld — Healthcare UX/UI trends 2025](https://www.excellentwebworld.com/healthcare-ux-ui-design-trends/)
- [TDP — design.md: a design system AI agents actually follow](https://designproject.io/blog/design-md-file/)
- [Nick Babich (UX Planet) — DESIGN.md best practices](https://uxplanet.org/design-md-best-practices-c00325e8b23a)
- [Design Systems Collective — The DESIGN.md template](https://www.designsystemscollective.com/the-design-md-405ca46e862c)

## 12. Shipped since implementation

The chat world is live in `previsit-intake.html`; these landed on top of it and are part
of the committed design:

- **`[W]` Splash** opens the app before the login gate: title "לקראת ביקורך במרפאה", one
  subtitle line, the journey illustration (300px, mirrored in RTL), and the CTA pinned to
  the bottom with the privacy link and language switch. Center-aligned, no panel, and no
  personal or clinical content of any kind pre-gate.
- **Illustration set.** Five hand-drawn sketches (royal-blue ink linework, one flat
  sky-blue circle accent): splash journey, login phone-with-bubbles, OTP envelope,
  capture page-in-viewfinder, sent paper plane. All render at 170px (splash 300px),
  always **below** their screen's content, embedded as quantized transparent PNGs
  (~115KB total); sources in `/illustrations`. The sent and splash planes mirror in RTL
  to fly in the sending/reading direction.
- **Motion.** Entrances only, gated to real transitions: the clinic "types" ~500ms before
  each message (composer disabled), bubbles rise, the just-sent answer pops, landing
  bubbles stagger, the progress bar grows via scaleX, menu and sheets slide, and the שלח
  plane flies off the button. Everything is transform/opacity ≤250ms and collapses under
  `prefers-reduced-motion`. No spinners, no confetti.
- **Chat scroll.** A new message parks at the top of the view with exactly half of the
  previous message visible above it; a computed spacer guarantees the position, and scroll
  survives intra-screen re-renders.
- **Sent** is a standalone summary page (title, still-to-bring, appointment, actions,
  illustration), no longer part of the conversation.
- **Login refinements.** Command-style instruction above the field, never-disabled
  Continue with a fixed-height amber inline error (the one deliberate error state),
  10-digit cap, centered OTP, bottom-centered language switch labeled in the target
  language.
- **Before/after record.** The pre-redesign wireframe screens are archived as PNGs in
  `docs/screens-before-redesign/` (captured from `main` at e6a0a0e).
