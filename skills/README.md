# `skills/` — the team's reusable Shared Skills

Four skills were built independently during the sprint, one per team member, and three of them
turned out to be three different slices of the same job: handling interview material honestly
when some of it is synthetic. This file records what each one was, how they compared, and what
the consolidation decided.

## What was found, and where

| Skill | Author | Where it was | State it was in |
|---|---|---|---|
| `interview-synth` | Matan | `skills/interview-synth/` | Correct: `SKILL.md` + `references/` + `assets/` |
| `interview-synthesis` | Anat | `skills/interview-synth/interview-synthesis.skill` | A zipped `.skill` bundle committed inside another skill's folder, then deleted |
| `interview-synthesis-anat` | Anat | `skills/interview-synthesis-anat/SKILL.md` | The unpacked re-upload of the above. Identical except the `name:` field |
| `interview-synth-Gal` | Gal | `skills/interview-synth-Gal` | A loose file with no extension, no folder, and no YAML frontmatter, so it could not load as a skill at all |
| `progress-tracking` | Mikhail | `.claude/skills/progress-tracking/SKILL.md` | Correct structure, but a different topic and a different directory from everything else |

## How the three interview skills compared

**They do not overlap, they adjoin.** Matan's generates synthetic interviews, Anat's turns
transcripts into graded findings, Gal's replays interviewed stakeholders against a new idea. Laid
end to end they are the actual workflow: fill a gap, synthesize the pile, pressure-test the
concept that comes out.

**They independently converged on the same core rule**, which is the strongest signal that the
merge is right. Matan's says synthetic material is "excluded from participant counts and from the
weight of any finding". Anat's says "synthetic sources don't count toward the corroboration
number, no matter how many there are". Gal's says panel feedback "never counts toward the
two-source rule". Three people, three skills, one rule, stated three times in three vocabularies.

**Where they conflicted was vocabulary, not substance.** Matan's graded synthetic output as
"directional / to confirm". Anat's had a four-tier ladder: Finding, Directional, Directional
(synthetic only), Single-source observation. Gal's had no grading vocabulary at all, just a flat
"not evidence". The consolidation adopts Anat's ladder as the single vocabulary, because it is
the only one that also handles the real-source-only cases, and it is the one the Research Report
needs.

**What each contributed uniquely.** Matan's brought the grounding evidence base (digital twins
beat profile personas, with citations), the four documented failure modes, the PII wall, and a
full worked example. Anat's brought the ingest-anything step, the source-classification step that
runs *before* content is read, and the two-layer output. Gal's brought the sharpest
when-not-to-use list in the set, and the honest note that a panel mixes real-grounded and
synthetic voices at different strengths.

**The naming was the worst problem.** `interview-synth` and `interview-synthesis` differ by four
characters and mean opposite things: one *makes* interviews, one *reads* them. Any model, and
most teammates, would pick the wrong one. That alone justified consolidating rather than shipping
three siblings.

## What the consolidation did

`skills/interview-synth/` is now one skill with three modes: **Generate**, **Synthesize**, and
**Panel**, sitting on one shared evidence ladder and one shared set of guardrails (ground before
generating, label permanently, no identifiable patient data, never simulate a group you never
interviewed, disclose provenance). The three duplicated statements of the "synthetic never
counts" rule became one, stated once and referenced by all three modes.

Nothing was dropped. Every substantive rule from all three sources survives in the merged skill.
The originals remain in git history, and the pre-merge copies were moved to `_to_delete/`.

## Open items

- `progress-tracking` (Mikhail's) still lives in `.claude/skills/`. It is a different topic and
  was left alone, but the team should pick one directory convention. Note that Claude Code
  auto-discovers `.claude/skills/`, not `skills/`, so skills in `skills/` need a symlink or an
  explicit path to load automatically.
- `_to_delete/` holds the superseded originals and can be removed once the team has reviewed the
  merge.
