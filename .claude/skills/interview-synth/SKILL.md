---
name: interview-synth
description: The team's single skill for working with synthetic and real interview material across user research, UX research, clinical/HCI research, customer discovery, and stakeholder interviews. Generate grounded, clearly-labelled synthetic interviews when a segment can't be reached yet; synthesize a pile of transcripts into an evidence-weighted findings report that never lets synthetic sources inflate a claim; or convene a stakeholder panel that reacts to an idea in the voices you actually interviewed. Use whenever someone asks for a "synthetic interview", "synthetic user", "synthetic persona", a mock or practice participant, or a rehearsal of a discussion guide; whenever transcripts, debriefs, or field notes need to be turned into themes or findings, even phrased as "here are my interviews, what did we learn"; whenever someone wants to check whether a claim is actually supported by enough independent sources, or wants real participant data separated from synthetic or generated data before presenting it; whenever someone asks "what would our stakeholders say about this" before committing to a concept; and whenever synthetic qualitative material is about to be produced or consumed at all, so it stays labelled and never gets mistaken for real evidence.
---

# interview-synth

One skill, three modes, one shared discipline.

Qualitative research is only as trustworthy as the bookkeeping behind it. The failure mode is
always quiet: a single vivid quote, or worse a model-generated one, gets treated a few
paragraphs later as if it were a validated pattern. Everything here exists to make that jump
visible and stop it from happening by accident.

## The three modes

| Mode | Use it when | Produces |
|---|---|---|
| **A. Generate** | A segment can't be reached yet, or a discussion guide needs piloting, or a one-sided finding needs pressure-testing | A labelled synthetic transcript plus hypotheses to verify |
| **B. Synthesize** | Transcripts, debriefs, or field notes need to become themes and claims | A findings table plus a narrative report, with every claim graded |
| **C. Panel** | An idea needs stress-testing against the people you already interviewed, before switching costs rise | Short in-voice reactions from each stakeholder, tied to their quotes |

They chain: generate to fill a gap, synthesize everything real and synthetic together with the
grades kept straight, then panel the concept that comes out of it. Pick the mode from what the
user is asking for; if it is ambiguous, ask once rather than guessing.

## The evidence ladder, which governs all three modes

Every claim this skill ever emits carries one of four grades. This is the backbone. Nothing
below overrides it.

- **Finding**, at least 2 independent **real** sources agree. The default threshold is 2. The
  user may set a different one; ask if the source pool is unusually small or large.
- **Directional**, fewer than the threshold in real sources, with synthetic sources also
  pointing the same way. Say explicitly what the split is, for example "1 real + 3 synthetic".
- **Directional (synthetic only)**, no real corroboration yet. Still surface it. It is the best
  possible next question for a real participant, not something to bury in an appendix.
- **Single-source observation**, one real source, no synthetic backup. Keep it visible, it may
  be exactly right, but never dress it up as a Finding.

Three consequences that are not negotiable:

1. **Synthetic sources never count toward the corroboration number.** No stack of them, however
   tall, pushes a claim into Finding status.
2. **Participant counts are real people only.** Five real plus three synthetic is "five
   participants", never eight.
3. **Panel output (Mode C) is not evidence at all.** It is rehearsal. It never appears in a
   findings table, never counts toward the threshold, and if it is described in a document at all
   it is labelled as rehearsal, not as a result.

If a synthetic claim is later corroborated by a real source, promote *that*: cite the real
evidence and drop the synthetic crutch.

## Shared guardrails

**Ground before you generate.** Studies of AI-simulated users find that "digital twins" built
from real interview transcripts track actual people far more closely, and carry substantially
less demographic bias, than "synthetic users" conjured from a demographic profile alone. Feed
the model real evidence and you get a useful stress-test. Feed it a stereotype and it hands the
stereotype back with confidence. See `references/background.md`.

**Label everything, permanently.** Every synthetic artifact carries the marker
`[SYNTHETIC — NOT REAL EVIDENCE]` in its title and in its filename, for example
`SYNTHETIC_family_interview_01.md`. The real-or-synthetic classification attaches to every
quote the moment it is extracted and survives all the way to the final output.

**No identifiable patient data, in either direction.** In a clinical context this is a
compliance wall, not a preference. Into the model: de-identify real transcripts first, stripping
names, ID numbers, dates of birth, contact details, exact locations, and anything else that
fingerprints a real child or family. Out of the model: the synthetic participant is a fictional
composite, never a portrait of a real identifiable person. Synthetic is not the same as
anonymised-real; if a detail would let someone recognise an actual patient, change it.

**A voice needs a source.** Modes A and C both invent a voice, but they need different things
behind it. Mode A exists precisely to reach a segment you have not interviewed, so it is allowed
there, and the grounding comes indirectly: what other stakeholders said about that segment, the
discussion guide written for them, desk research. The thinner that indirect grounding, the harder
you hedge. Mode C is stricter, because a panel replays positions rather than exploring them: a
stakeholder gets a seat only if there is a transcript to quote, real or synthetic-and-labelled. A
group with neither, such as secretaries and admin when nobody has spoken to one, gets no seat,
because the panel would invent a position rather than replay one.

**Disclose provenance wherever synthetic material is used.** What model, what date, what real
material grounded it.

---

## Mode A, generate a grounded synthetic interview

A synthetic interview is a simulated research conversation: the model plays a participant, and
if useful the interviewer, to produce a realistic transcript. It is a thinking tool, not data.

### Use it for, and not for

Use it for preliminary, hypothesis-shaped work only: surfacing hypotheses to take to real
people, piloting a discussion guide to find dead questions, bad ordering, and leading phrasing
before spending a real participant on them, getting oriented in an unfamiliar domain, building
proto-personas to refine against real data, and stress-testing a one-sided finding, for example
when you have clinicians but no families.

Do not use it to replace real research or paper over a recruiting gap, to validate a concept or
make a design or business decision, to model niche or under-documented populations, which is
exactly where the model fabricates most, or to produce numbers or anything else that reads as a
finding. If a request is really one of these, say so and offer the synthetic version as a
clearly-scoped stopgap.

### Gather grounding first

Do not start writing until you have: real interviews, transcripts, or debriefs already
collected, which is the strongest grounding; desk research and any landscape scan; the
discussion guide for the stakeholder being simulated; and the specific gap and goal, meaning
which segment, which questions most need pressure-testing, and what decision this is not allowed
to drive. If little grounding exists, generate anyway but widen the uncertainty: shorten the
interview, hedge harder, and flag that it is closer to a stereotype than a twin.

### Workflow

1. **Frame the job.** One line on who is being simulated, why, and what real material grounds
   it. Confirm this is preliminary use, not validation.
2. **Build the participant from evidence.** Derive their situation from the grounding, not from
   clichés. Give them a concrete recent episode, because realism lives in specifics ("last
   Tuesday he woke at 2am coughing"), not adjectives.
3. **Run the guide.** Follow the real discussion guide's spine: consent, warm-up, current
   process, a concrete recent example, what breaks, what would help, wrap-up. Let the interviewer
   probe follow-ups the way a good moderator would.
4. **Engineer against the four failure modes** below.
5. **Label and separate.** Marker top and bottom, own file, own folder, away from real data.
6. **Extract hypotheses, not findings.** End with a short list of claims to verify with real
   people, never "what we learned".

### The four failure modes to engineer against

1. **Sycophancy.** Real participants push back, misunderstand the question, dislike the idea, and
   wander off-topic. Bake in friction: at least one point where the participant disagrees, is
   confused, or wants something you did not offer. A synthetic interview where everyone loves the
   concept is worthless.
2. **Homogenization.** Synthetic respondents cluster near the average and miss the edges. When
   generating more than one, force real diversity across literacy, language, attitude, and
   competence, and include at least one deliberate edge case, not three reskinned copies of the
   mean.
3. **Shallow generic lists.** Left alone the model emits tidy lists of plausible needs with no
   priority and no when, why, or how. Force depth: make the participant rank, hesitate,
   contradict themselves, and tell stories. Asked "what's hardest", a real person names one
   concrete thing and gets specific, not a bulleted five.
4. **Overclaimed realism.** The output sounds like data, which is precisely the danger. Keep the
   register human ("wheezing", not "expiratory stridor"), keep memory imperfect, and never let
   polish imply reliability.

### Output shape

```
# [SYNTHETIC — NOT REAL EVIDENCE] Interview: <segment>, <one-line situation>

Provenance: generated by <model> on <date>, grounded in <real sources>.
Purpose: <hypothesis generation | guide pilot | stress-test | proto-persona>.
NOT to be used for: validation, decisions, or participant counts.

## Transcript
**Interviewer:** ...
**<Participant>:** ...
(consent, warm-up, current process, concrete recent example, what breaks,
 what would help, wrap-up, with probing throughout)

## Hypotheses to verify with real participants
- <claim> -> how we would check it with a real person

## Where this is most likely wrong
- <the parts least grounded and most invented>
```

`assets/SYNTHETIC_family_interview_example.md` is a complete filled-in example following this
exact template. Read it to see the friction, the vernacular, the imperfect memory, and the
hypotheses-not-findings ending in full.

### Worked micro-example

**Prompt:** "We interviewed pulmonologists and a nurse but couldn't recruit families in time.
Make a synthetic caregiver interview so we can pressure-test the clinician-only picture."

**Good response:** Gather the real clinician debriefs and the family discussion guide, simulate
one caregiver of a specific child with a concrete recent episode, run the family guide with real
probing, include a moment where the caregiver misunderstands "triggers" and one where they resent
being told to "bring everything", end with 4 or 5 hypotheses ("caregivers may not know what
'relevant history' means", verify by asking real caregivers to sort documents), label the file
`SYNTHETIC_family_interview_01.md`, keep it out of the participant count, and grade anything it
raises as Directional (synthetic only).

**Bad response:** A polished, agreeable transcript where the caregiver articulately confirms
every clinician claim, presented alongside real interviews as an eighth "participant".

---

## Mode B, synthesize transcripts into an evidence-weighted report

### Step 1, ingest every transcript

Transcripts arrive as plain text, markdown, PDF, docx, even photos of handwritten notes.
Auto-detect per file and read with the right tool: `.txt` and `.md` directly, `.pdf` via the pdf
skill, `.docx` via the docx skill, images visually. Never ask the user to convert files first;
that friction is exactly what this removes.

### Step 2, classify each source before reading it for content

For every transcript determine the **participant role and setting**, for example "pediatric
pulmonologist, Clalit", anonymising a real name to role plus setting if the user has not already
done so; and whether it is **real or synthetic**. A source is synthetic if it was generated by
an LLM, is a hypothetical or composite persona, or is otherwise not an actual recorded
conversation with a real person. Look for explicit labels first. If a transcript's status is
genuinely ambiguous, ask rather than guess: this classification is load-bearing, and a wrong
guess here silently corrupts every count downstream.

### Step 3, write a per-interview debrief

Extract observations in the source's own language; do not paraphrase away specificity. If an
interview guide or topic spine exists, organise around it, otherwise around whatever structure
the conversation actually took. Pull direct quotes with enough surrounding context to know what
question prompted them.

### Step 4, cluster into candidate themes

Group observations that point at the same underlying claim even when the wording differs a lot,
because clinicians rarely phrase the same complaint the same way. Note contradictions explicitly
rather than smoothing them over: a disagreement between two sources, or between a source and a
record, is often itself the finding.

### Step 5, apply the evidence ladder

Grade every candidate theme using the ladder at the top of this document. Nothing else.

### Step 6, produce both layers in one document

**Findings table**, for fast review:

| # | Claim | Status | Supporting sources | Representative quote |
|---|---|---|---|---|
| 1 | [one-sentence claim] | Finding / Directional / Directional (synthetic only) / Single-source | [count, real vs synthetic breakdown] | "[quote]", [role, setting] |

**Narrative report**, one section per row, strongest status first. Each section states the claim
plainly, gives 2 to 4 sentences of context, quotes with attribution, and where relevant the
contradiction or nuance that makes it interesting rather than obvious.

Close with a short **Guardrails and gaps** note: what threshold was used, how many real versus
synthetic sources went in, and which Directional items most need a real source next.

Default to a single markdown file holding both layers, so it is easy to skim and easy to hand to
teammates. If the request implies a fuller deliverable ("write this up as our research report"),
fold the same table and narrative into that report structure rather than producing two separate
documents.

### Translated transcripts

Translate quotes when the output language differs, but flag them as team or AI translations, for
example by appending ", translated". Never present a translation with the same confidence as a
verbatim quote.

### Why not to skip steps

It is tempting to jump straight to polished-sounding findings, because the raw material is right
there and the model writes well. Resist. The value here is not the prose, it is the bookkeeping:
keeping every claim honestly tied to how many independent real people actually said it. A report
that reads confidently but quietly promotes one quote to "the pattern" misleads exactly the
people relying on it to make product or clinical decisions. When in doubt about whether something
clears the bar, err toward labelling it Directional and say why, because that is more useful than
a false Finding.

---

## Mode C, stakeholder panel

An idea goes in, and everyone you interviewed responds to it.

### How it works

1. The user describes the idea in two lines.
2. Load the quote bank and assemble a panel from the stakeholders actually interviewed:
   physician, nurse, family, mentor.
3. Each responds in their own voice, grounded in what they actually said. Positive, negative, or
   both. The goal is to surface problems while they are still cheap to fix, and to steer toward a
   version that holds up for everyone involved.

### Use it when, and not when

Use it before committing to a concept direction while switching costs are low, before investing
days in a prototype flow, when prepping for demo Q&A or a mentor review to find the question you
cannot answer, and when the team is split between two ideas and arguing from opinion.

Do not use it as a substitute for a real conversation; if the stakeholder is reachable, go ask
them. Do not use it as evidence in the report; panel feedback is rehearsal, and it never counts
toward the corroboration threshold. Do not run it on groups you never interviewed, such as
secretaries and admin, because it would invent a voice you do not have. Do not use it in early
divergent ideation, where you still want quantity, or for usability questions, which need a test
with a person.

### The honest limitation

A panel voice is only as strong as its source. Voices built from real transcripts replay real
positions; a synthetic voice, such as the family voice when no family has been interviewed, is
labelled synthetic and is a lead to check, never a finding. Say which is which on every panel.

### Output shape

Three or four lines per stakeholder, in their voice, each tied to the quotes it rests on. Nothing
else: no scores, no rankings, no synthesis.

Example of the register:

> **Pulmonologist:** The structured basics are the real win. Family history, who smokes, where
> the child was born, that eats long minutes today. But I'll still cross-check anything the
> family types against the documents, so don't promise me it replaces that.
>
> **Nurse:** If it arrives before the visit instead of on a clipboard in the waiting room, my
> intake starts much further along. What worries me is that I linger on what parents brush off,
> like shortness of breath they blame on weight, and a form doesn't know how to push back.
>
> **Family (synthetic):** Being told specifically what to bring would have helped. Last time I
> was told I didn't need anything, then handed a form with a baby in my arms.
>
> **PM mentor:** Reads as still top of funnel, which is right. Make sure you can measure it
> against the current process, or the demo proves nothing.

Constraints count as feedback too, and are often the most valuable line on the panel. A
pulmonologist saying "wherever this data sits, an identified document can't go into a model, that's
not a preference, it's the line" is worth more than five reactions to the interface.

---

## How synthetic material appears downstream

- Excluded from participant counts and from the weight of any finding.
- In a report, synthetic material lives in its own clearly-labelled block or appendix, and any
  hypothesis it raises is written as directional or to-confirm, never as a result.
- Provenance disclosed wherever it is used.
- Panel output does not appear in the report at all.

## Further reading

`references/background.md`, the evidence base behind the grounding rule and the four failure
modes, with full citations.

`assets/SYNTHETIC_family_interview_example.md`, a full labelled sample interview to copy the
shape and register from.
