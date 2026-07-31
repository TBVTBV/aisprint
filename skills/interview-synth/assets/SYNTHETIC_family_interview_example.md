# [SYNTHETIC — NOT REAL EVIDENCE] Interview: Caregiver, mother of an 8-year-old with recurring breathing trouble

Provenance: generated as a worked example for the `interview-synth` skill, grounded in the
project's real pediatric-pulmonologist and nurse debriefs and the family discussion guide.
Purpose: worked example + stress-test of the clinician-only picture from the family side.
NOT to be used for: validation, decisions, or participant counts. This is a hypothesis
generator, not a participant.

> Read this alongside `../SKILL.md`. Notice the things a good synthetic interview does that a
> naive one doesn't: the participant **misunderstands a question**, **pushes back**, **can't
> remember** specifics, speaks in **everyday words** not medical ones, and tells a **concrete
> story** instead of listing tidy needs. The value is the friction, not the agreement.

## Transcript

**Interviewer:** Thanks for making the time. We're master's students looking at how a child's
history reaches the clinic before a visit — we're not selling anything and there are no wrong
answers. It's voluntary, you can skip anything, and nothing here identifies you or your child.
Okay to carry on?

**Caregiver:** Yeah, that's fine.

**Interviewer:** Tell me a bit about your son and what brings him to the pulmonology clinic.

**Caregiver:** So he's eight. It started — I want to say two years ago? He'd get these coughs
that just wouldn't quit, especially at night, and once he went kind of blue-ish around the lips
after running around at a birthday party and that really scared me. The GP sent us to a
specialist, and now we go every few months. They think it's asthma but honestly I'm still not a
hundred percent sure what the official word is. Nobody's ever really sat me down and said "here's
the name of it."

**Interviewer:** When you have an appointment coming up, what do you do to get ready?

**Caregiver:** *[laughs]* Panic, a little. There's a letter they send with the appointment and it
says something like "please bring relevant documents and any imaging." And I always think — okay,
what's relevant? I don't know what's relevant. So I just take everything. I've got this plastic
folder, I shove in whatever I can find — old prescriptions, a disc from an X-ray we did once at a
private place, a page the hospital gave us that one time. And then half of it they don't even
look at and I feel a bit silly.

**Interviewer:** You mentioned a disc from a private place. Walk me through where your son's
medical records actually live, from your side.

**Caregiver:** Honestly? Everywhere and nowhere. There's the health fund app on my phone, that's
got some of it — but not the time we ended up in the ER on holiday, that's not in there at all,
because it was a different hospital. The private X-ray, that's the disc, which — who even has a
thing to read a disc anymore. Some of it's just in my head. Like I know he was on a stronger
medicine for a while after a bad winter, but the name? No idea. It was the purple one. Or maybe
that was the inhaler. See, this is what I mean.

**Interviewer:** Let me ask about the last visit specifically. Can you take me through it — what
they asked, what you could answer, what you couldn't?

**Caregiver:** Right, so the last one was a couple of months ago. The doctor asked how often he's
using the blue inhaler — the rescue one — and I genuinely didn't know the number. Like, "a lot"?
Some weeks nothing, then a bad week and it's every day. I felt like I was being tested and
failing. She asked about triggers and I didn't really — I wasn't sure what counted. I said "the
cold, and running," but afterwards in the car I remembered he's always worse at my mum's, and
she's got two cats, and I thought, oh, that's probably a trigger isn't it, and nobody had that.

**Interviewer:** That's really useful. When you say you "weren't sure what counted" — if someone
had asked you those questions *before* the visit, at home, would that have gone differently?

**Caregiver:** Probably, yeah. If I'd had them the night before I could've actually looked — gone
through the app, asked my husband, counted properly instead of guessing on the spot with the
doctor staring at me. Although — I'll be honest, if it's some long form with a hundred questions
I'm not filling that in. I've got two other kids. It'd have to be quick, and it'd have to feel
like it mattered.

**Interviewer:** What did you expect the doctor could already see on their screen when you walked
in?

**Caregiver:** Everything, kind of? That's the thing that surprised me. I assumed it was all in
"the system," you know, the computer, that they'd pull him up and it'd all be there. And then she's
asking me for the X-ray on the disc and I'm thinking — you can't see it? I brought it but I
assumed it was already there. That threw me a bit.

**Interviewer:** If you could change one thing about how the whole before-the-visit part works,
what would it be?

**Caregiver:** Someone telling me, plainly, what actually matters. Not "bring relevant documents"
— which relevant documents. "Bring the number of times he used the blue inhaler this month. Bring
this specific paper from the ER." If someone gave me a short list of the exact things, I'd get
them, gladly. It's not that I don't want to help — I'd move mountains for him — it's that nobody
tells you the rules and then you feel like the disorganised parent.

**Interviewer:** Is there anything I should have asked and didn't?

**Caregiver:** Maybe — the language thing? Not for me, but my mum, who takes him sometimes, her
Hebrew isn't great and she wouldn't fill in a form or know the medicine names at all. So whoever's
bringing him matters. Sometimes it's not me in the room.

**Interviewer:** Thank you — this was genuinely helpful.

## Hypotheses to verify with real participants

- Caregivers may not share the clinic's meaning of "relevant" and default to
  "bring everything / hope for the best." → Verify: ask real caregivers to sort a pile of
  documents into "the doctor needs this" vs. "not needed" and see where they struggle.
- Concrete, countable, recent asks (reliever uses this week; nights woken) may be answerable at
  home but not on the spot. → Verify: A/B a short pre-visit prompt vs. in-room recall with real
  families and compare accuracy.
- Caregivers may assume the record is already complete on the clinic's screen (mirrors the
  clinician-reported "we thought you see everything on the computer"). → Verify directly with
  real caregivers.
- Triggers and cross-setting exposures (the grandmother's cats) may live only in the parent's
  head and surface only after the visit. → Verify: does a structured trigger checklist recover
  them?
- The person who physically brings the child (grandparent, limited Hebrew) may not be the person
  who holds the information. → Verify: who actually attends, and what they know.

## Where this is most likely wrong

- The emotional register ("panic," "failing a test") is plausible but invented — real caregivers
  may frame the pre-visit moment very differently, or not find it stressful at all.
- The specific record-fragmentation details (health-fund app, private disc, out-of-network ER)
  are lifted from *clinician* accounts of what families carry — a real caregiver's map of their
  own records could look nothing like this.
- Willingness to fill in a pre-visit form is asserted here; real drop-off, literacy, and
  motivation are exactly the things this cannot tell us and a real study must.
- One synthetic voice cannot represent the range of families — this is a single, average-ish
  case and deliberately not an edge case; generate more, with real diversity, before trusting any
  pattern.
