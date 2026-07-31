---
name: interview-synth
description: Generate grounded, clearly-labeled synthetic UX research interviews (a simulated participant plus interviewer) from real evidence — for hypothesis generation, piloting a discussion guide, stress-testing early findings, and building proto-personas when a real segment can't be reached yet. Use this whenever someone asks for a "synthetic interview", "synthetic user", "synthetic persona", an "AI-generated interview", a mock or simulated participant, a practice interview to rehearse a guide, or wants to fill a stakeholder gap (e.g. "we interviewed clinicians but no families yet"). Also invoke it whenever synthetic qualitative data is about to be produced at all, so it is generated responsibly, grounded in real inputs, and never mistaken for real research evidence.
---

# Interview-Synth — grounded synthetic UX interviews

**The repetitive task this captures:** writing a realistic practice / synthetic interview by hand every time you need to pilot a discussion guide, explore a segment you can't reach yet, or pressure-test a one-sided finding — so it is done well *and safely* each time instead of improvised from scratch.

## The one rule that governs everything

A synthetic interview is a *simulated* research conversation: the model plays a participant (and, if useful, the interviewer) to produce a realistic transcript. It is a thinking tool, **not data**. Everything below exists to protect two things at once:

1. **Ground it in real material** so the output reflects your problem space, not the model's stereotypes.
2. **Never let it be mistaken for real evidence** — in the artifact, in counts, or in a report.

Why grounding is not optional: studies of AI-simulated users find that "digital twins" built from *real interview transcripts* track actual people far more closely — and carry substantially less demographic bias — than "synthetic users" conjured from a demographic profile alone. Feed the model real evidence and you get a useful stress-test. Feed it a stereotype and it hands the stereotype back with confidence. (See `references/background.md`.)

## When to use it — and when not to

Use it for **preliminary, hypothesis-shaped work only**:

- **Surface hypotheses** to take to real people ("what might a caregiver say that our clinicians can't tell us?").
- **Pilot a discussion guide** — find dead questions, bad ordering, and leading phrasing before spending a real participant on them.
- **Get oriented in an unfamiliar domain** before the first real session.
- **Build proto-personas** as a starting point to refine against real data.
- **Stress-test a one-sided finding** — e.g. you have clinicians but not families, and want to pressure-test whether a clinician-reported claim holds up from the other side.

Do **not** use it to:

- **Replace real research**, or fill a recruiting gap and move on as if the segment were covered.
- **Validate** a concept, or make a design/business decision.
- **Model niche, specialized, or under-documented populations** — exactly where the model has least to draw on and fabricates most.
- **Produce numbers** or anything that reads as a finding.

If a request is really one of the "do not" cases, say so and offer the synthetic version as a clearly-scoped stopgap, not a substitute.

## Inputs — gather grounding before you generate

Do not start writing until you have grounding material. The richer the input, the less the model invents. Ask for, or assemble:

- **Real interviews / transcripts / debriefs** already collected (the strongest grounding — this is what makes it a "twin" rather than a stereotype).
- **Desk research and any landscape/competitive scan** relevant to the segment.
- **The discussion guide** for the stakeholder you're simulating (the interview should be driven by it).
- **The specific gap and goal** — which segment, which questions you most want pressure-tested, and what decision this is *not* allowed to drive.

If little grounding exists, generate anyway but **widen the uncertainty**: shorten the interview, hedge harder, and flag that it is closer to a stereotype than a twin.

## Workflow

1. **Frame the job.** State in one line who is being simulated, why, and what real material grounds it. Confirm this is a preliminary use, not a validation.
2. **Build the participant from evidence.** Derive their situation from the grounding, not from clichés. Give them a concrete recent episode to talk about — realism lives in specifics ("last Tuesday he woke at 2am coughing"), not adjectives.
3. **Run the guide.** Follow the real discussion guide's spine: consent → warm-up → current process → a concrete recent example → what breaks → what would help → wrap-up. Let the interviewer probe follow-ups, exactly as a good moderator would.
4. **Engineer against the four failure modes** (next section) as you write — this is where synthetic interviews usually go wrong.
5. **Label and separate.** Mark every artifact as synthetic, top and bottom. Keep it in a separate file/folder from real data.
6. **Extract hypotheses, not findings.** End with a short list of *claims to verify with real people*, never "what we learned."

## The four failure modes to engineer against

These are the documented ways synthetic interviews mislead. Counter each deliberately.

**1. Sycophancy — the model agrees with everything.** Real participants push back, misunderstand the question, dislike your idea, and go off-topic. Bake in friction: at least one point where the participant disagrees, is confused, or wants something you didn't offer. A synthetic interview where everyone loves the concept is worthless.

**2. Homogenization — every synthetic person clusters on the "average."** Synthetic respondents show far lower variance than real ones and miss the edges. When generating more than one, force genuine diversity — different literacy, language, attitude, competence, and at least one deliberate *edge case* — rather than three lightly-reskinned copies of the mean.

**3. Shallow, generic lists.** Left alone the model emits long tidy lists of plausible-sounding needs with no priority and no "when / why / how." Force depth: make the participant rank, hesitate, contradict themselves, and tell stories instead of listing. If asked "what's hardest," a real person names one concrete thing and gets specific — not a bulleted five.

**4. Overclaimed realism.** The output *sounds* like data, which is precisely the danger. Keep the register human (vernacular, not textbook vocabulary — "wheezing," not "expiratory stridor"), keep memory imperfect, and never let the transcript's polish imply reliability it doesn't have.

## Guardrail — no identifiable patient data (PII)

A hard line in **both** directions. In a clinical context this is a compliance wall, not a preference: identifiable patient data must never enter an LLM.

- **Into the model:** never paste identifiable data as grounding. De-identify real transcripts and documents first — strip names, ID numbers, dates of birth, contact details, exact locations, and anything else that fingerprints a real child or family — *before* feeding them in.
- **Out of the model:** the synthetic participant is a *fictional composite*, never a portrait of a real, identifiable person. Synthetic is not the same as anonymised-real — if a detail would let someone recognise an actual patient, change it.

Getting this right is also what keeps the output usable without a privacy review, and keeps faith with the real people whose data grounds it.

## Output format

Produce two things: the transcript, then a short synthesis. Use this shape:

```
# [SYNTHETIC — NOT REAL EVIDENCE] Interview: <segment>, <one-line situation>

Provenance: generated by <model> on <date>, grounded in <list real sources>.
Purpose: <hypothesis generation | guide pilot | stress-test | proto-persona>.
NOT to be used for: validation, decisions, or participant counts.

## Transcript
**Interviewer:** ...
**<Participant>:** ...
(consent → warm-up → current process → concrete recent example → what breaks →
 what would help → wrap-up; interviewer probes throughout)

## Hypotheses to verify with real participants
- <claim> → how we'd check it with a real person
- ...

## Where this is most likely wrong
- <the parts least grounded / most invented>
```

Every synthetic artifact keeps the `[SYNTHETIC — NOT REAL EVIDENCE]` marker in its title and filename (e.g. `SYNTHETIC_family_interview_01.md`).

A complete, filled-in example that follows this exact template — the friction, the vernacular, imperfect memory, and the hypotheses-not-findings ending, all in full — is in `assets/SYNTHETIC_family_interview_example.md`. Read it to see what "good" looks like end to end.

## Reporting rules (how it appears downstream)

- **Excluded from participant counts and from the weight of any finding.** Five real + three synthetic is "five participants," never eight.
- In a report, synthetic material lives in its **own clearly-labelled block or appendix**, and any hypothesis it raises is written as *directional / to confirm*, not as a result.
- If a synthetic claim is later **corroborated by a real source**, promote *that* — cite the real evidence and drop the synthetic crutch.
- Disclose provenance (what model, what grounding) wherever the synthetic data is used.

## Worked micro-example

**Prompt:** "We interviewed pulmonologists and a nurse but couldn't recruit families in time. Make a synthetic caregiver interview so we can pressure-test the clinician-only picture."

**Good response:** Gather the real clinician debriefs + the family discussion guide → simulate one caregiver of a specific child with a concrete recent episode → run the family guide with real probing → include a moment where the caregiver misunderstands "triggers" and one where they resent being told to "bring everything" → end with 4–5 hypotheses ("caregivers may not know what 'relevant history' means" → verify by asking real caregivers to sort documents) → label the file `SYNTHETIC_family_interview_01.md`, keep it out of the participant count, and mark its findings directional.

**Bad response:** A polished, agreeable transcript where the caregiver articulately confirms every clinician claim, presented alongside real interviews as an eighth "participant."

## Further reading

`references/background.md` — the evidence base (NN/g guidance, digital-twin vs. synthetic-user studies) and full citations for the claims above.

`assets/SYNTHETIC_family_interview_example.md` — a full, labelled sample interview to copy the shape and register from.
