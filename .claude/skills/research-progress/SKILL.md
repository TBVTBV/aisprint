---
name: research-progress
description: Compare the Group 7 research plan against the actual files in the team's Google Drive and report which deliverables are complete, which are partial, and which are missing. Use when the user asks where the research stands, what is left to do, what is outstanding, whether the team is on track, or asks for a progress check against the plan.
---

# Research progress check

## Locations

All locations are in Google Drive. Never read the local copies in this project — they are
stale downloads kept for convenience, and Drive is the single source of truth.

| | Name | ID |
|---|---|---|
| Project root | `Group 7 - Gal, Anat, Mikhail, Yarden, Matan` | `1JWMNO1HXta6rOKVPGaXJpu6NQUALRYJF` |
| Plan doc | `Research_Plan_FINAL.pdf` | `1j3JRiBBuBnJFcBr-ziJFWoPFcbJWnpjf` |

**Scan these, recursively:**

| Folder | ID |
|---|---|
| `Deliverables/` | `1JsQStRvGb_tj5W1u4l7v6pvtTWrPz3I4` |
| `Interviews/` | `15E4zlLDzeb5WWtWr9mzVQKzfx1hTDrUx` |
| `Interviews/Interview Guides:Protocols/` | `17rAUmM1Kse7z4WQxTNG6hYwIUS9RPsES` |
| `Interviews/Preperatory:Mentor Interviews/` | `11k3F6PceYehkkcIl299sWHOhGvWnZIFX` |
| `Synthesis/` | `1aiApFO1X6E7-P8iUZDa9198eg9J0Hxvw` |

**Skip:** `Course materials/` (not team output), `Reviews/` (feedback on other groups),
`Skills/` (tooling).

A Google Doc named `Research Plan — Pediatric Pulmonology (Pre-Visit Intake)` also sits in
`Deliverables/`. It is superseded — do not read it as the plan. If it is ever modified more
recently than `Research_Plan_FINAL.pdf`, say so in one line at the end of the output, but
still use the PDF for the run.

## Steps

1. **Read the plan and take §9 as the checklist.** Section 9, "Outputs & Definition of Done",
   lists the deliverables. Use those items verbatim as the checklist rows, in order. Ignore
   §1–§8 for the checklist itself — they are context, not deliverables.

2. **Take owners only where the plan states them.** §9 items carry no owners. §8 has a "Team
   roles" table and a one-week timeline with named milestone owners. Only fill the Owner
   column when the plan names an owner for that specific deliverable; otherwise leave it
   blank. Never carry a role owner across to a deliverable they were not assigned.

3. **List the files.** Walk every scan folder and pull each file's name, last-modified date,
   and last-modifying user from Drive metadata.

4. **Match, allowing many-to-one in both directions.** A §9 deliverable is frequently
   satisfied by a *section inside* a larger document rather than a file of its own, and one
   file may satisfy several deliverables. Open the substantial documents and look for the
   content, not for a matching filename. If a deliverable has no plausible candidate, or two
   equally plausible ones, mark ❓ and carry it to step 6.

5. **Judge each deliverable against its own wording, including qualifiers.** The plan's
   adjectives are requirements, not decoration:
   - "*per stakeholder*" — a map covering one stakeholder is partial, not done.
   - "*real* quotes" — material labelled SYNTHETIC does not satisfy it.
   - "*prioritised* list" — an unordered mention of the same items does not satisfy it.

   A deliverable is 🟡 when the content exists but under-delivers on a qualifier, and when a
   document states its own gaps, quote that self-description rather than re-judging it.
   Audio and video files cannot be assessed for substance — mark them ❓ rather than guess.

6. **Emit the checklist**, then list leftovers: files that matched no deliverable, and
   deliverables that matched no file.

## Output format

Open with a one-line count: `2 done · 2 partial · 1 unclear`

Then one table, one row per §9 deliverable, in plan order:

| | Deliverable | Owner *(plan)* | Where it lives | Last modified | Last edited by *(Drive)* |
|---|---|---|---|---|---|

- ✅ exists and meets the deliverable as worded
- 🟡 exists but under-delivers on a stated qualifier
- ❌ nothing found
- ❓ unclear — needs a human look

Add one short line under any 🟡 or ❓ row saying exactly what is missing. Then the two
leftover lists. Nothing else — no summary paragraph, no recommendations, no next steps
unless asked.

## Guardrails

- **Never assign a deliverable to anyone.** Owners come from the plan and nowhere else. A
  blank owner stays blank.
- **Never treat "last edited by" as "responsible for".** Drive says who touched a file; the
  plan says who owns it. Separate columns, and neither may be used to infer the other.
- **Never reconcile the team roster.** The Drive folder name lists five people; the plan and
  report name four. Report the discrepancy if it is relevant and let the team resolve it.
- **Never mark something done from its filename.** Steps 4 and 5 are not optional.
- **Never promote a leftover file into the checklist.** Unmatched files are listed as
  leftovers only. The checklist has exactly as many rows as §9 has items.
- **Never resolve an ambiguous match by guessing.** Use ❓ and state what is unclear.
- **Never read the local project copies** as a substitute for Drive, even when a Drive file
  is slow or awkward to open. Report the problem instead.
- **Read-only.** Do not create, rename, move, edit, or delete anything in Drive.
