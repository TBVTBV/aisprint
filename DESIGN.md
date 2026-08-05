# Design

<!-- impeccable:design-schema 1 · seed db4ae67f · mode operate -->

The visual system for Group 7's Session 2 artifacts, recorded from the built pages
(`Group7_S2_Synthesis.html`, `Group7_S2_Ideation.html`). These are two self-contained
files — inline CSS/JS, no build, no CDN, no network, no browser storage — that open by
double-click from a synced Google Drive folder. Product truth lives in `PRODUCT.md`; this
file owns the durable visual decisions.

## The world

A **pen-plotter instrument trace on graph paper.** The page is warm plotter paper with a
continuous fine grid (40px) and major rules (200px) drawn as fixed background gradients.
Regions are bounded by **hairline rules and channel baselines**, never by drop-shadowed
cards. A "channel" is the recurring structural device: a lane that begins on a 1px top rule,
the way a chart recorder writes one channel of a trace. There is one ink weight; depth comes
from rules and a single sunk surface, not from elevation.

**Thesis the system serves:** provenance is the visual system. Every observation shows its
source and its weight where it sits, and the synthetic half can be subtracted (a filter) to
watch which clusters still stand. Real and synthetic never share a treatment.

## Color

Restrained: warm neutral ground + graphite ink, with identity carried **only by data-mark
hues** on ticks, tags, traces and top-rules — never as decorative fills. Light values are the
CVD-validated, text-safe steps (all ≥5:1 as text on the surface).

| Role | Light | Dark |
|---|---|---|
| Paper / surface / sunk | `#f7f6f1` / `#fdfdfa` / `#f1efe7` | `#0e0e0c` / `#171714` / `#121210` |
| Ink 1–4 | `#14140f` `#45433c` `#63605a` `#8b887e` | `#f4f3ec` `#c4c1b6` `#9d9a90` `#7e7b72` |
| Rules (grid-fine, grid-major, rule, rule-soft) | `#e8e5da` `#d8d4c4` `#c9c5b6` `#e0dccf` | `#24231e` `#33322a` `#3a3931` `#2a2924` |
| Physician | `#1d5fae` | `#3987e5` |
| Nurse | `#0d7a52` | `#199e70` |
| Synthetic | `#b84714` | `#d95926` |
| Desk research | `#5d5a53` + 45° hatch | `#9d9a90` + hatch |
| Gate (disqualifier) | `#b23025` | `#e06a60` |

Source coding never rests on hue alone: every tick/tag/trace also carries a text label, and
the synthetic treatment adds a 135° hatch plus the word "synthetic". Theme follows
`prefers-color-scheme` and a manual toggle that stamps `data-theme` on `<html>`.

## Type

One workhorse sans stack (system UI), `font-variant-numeric: tabular-nums` globally. A fixed
rem scale (`--t-xs .6875rem` → `--t-2xl 2.375rem`), tight tracking on display
(`-0.03em` on h1), and **wide-tracked uppercase instrument labels** (`.lab`, `.14em`) used for
field labels, calibration keys and column headers. Instrument labels are a field-label device
only — never an eyebrow above a heading (craft-floor ban). Section names are folded into the
heading itself; section numbering lives in the sticky rail alone.

## Components & devices

- **Instrument masthead**, not a hero: title left, a tabular calibration readout right (real
  vs. synthetic counts kept honest), a sticky section rail beneath.
- **Affinity board:** a responsive column grid (6 → 3 → 2 → 1 across 1500/1080/760px) of
  cluster channels holding movable note slips. Each slip carries a colored source tick + text
  label; Hebrew-sourced quotes carry a `translated · HE` badge; desk-research notes render as
  em-dash **paraphrases** (never wrapped in `<q>`, since they are not verbatim). Full keyboard
  path: drag, or open the modal drawer and reassign cluster; the moved note is re-focused by id.
- **Drawer:** a committed modal (`aria-modal`, scrim, focus trap, Escape), not a half-modal.
- **Journey trace:** an SVG feeling line over a 4-level named axis (High/OK/Low/Lowest) with a
  per-stage feeling word in text; physician lane solid + disc markers, caregiver lane dashed +
  square markers (distinct beyond hue). Each lane keeps its own stage count.
- **Insights:** `<details>` disclosures, first open by default, with an explicit Open/Close
  affordance and the real-source count printed as text ("3 real sources").
- **Ideation concept grid:** de-selected concepts recede on the **surface** (`--sunk` ground,
  softened top-rule, body text to `--ink-3`) — never by opacity, so what was left behind stays
  legible. "Made of" lists are generated from the concept array so they cannot drift from the
  interaction. Empty state teaches recovery. Filter chips encode off with a dashed border and
  paper ground; text stays full contrast.

## Motion

Operate-mode restraint: 150ms state transitions on `--ease` (`cubic-bezier(.16,1,.3,1)`). The
one authored moment is the journey trace drawing in via `clip-path` on load; everything else is
state feedback. Respects `prefers-reduced-motion`.

## Rules that hold everywhere

- No kicker/eyebrow above any heading. No opacity below 0.6 to encode state. No shadowed cards
  as the structural container.
- Color never the sole carrier of meaning. Body/placeholder text ≥4.5:1 in both themes.
- Every claim carries its provenance on the surface; synthetic is labelled at every point of use
  and never counted as evidence.
- 2px radius throughout; one ink weight; hairline rules do the separating.

## Known replacements / open items

- Hebrew original-language text is not held in this repo; translated quotes are marked as
  `translated · HE` on the Clalit physician interview (the one PRODUCT.md names as Hebrew). The
  correct Hebrew nurse interview should also be marked `lang:"he"` once identified from the
  Drive quote bank, and originals attached where the quote bank preserves them.
- Content is locked to the `.docx` versions; the HTML is a rendering, not a rewrite.
