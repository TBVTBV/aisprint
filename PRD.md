# PRD: Beforehand, low-fidelity clickable web app

**Group 7 · AI Product Sprint 2026 · Challenge #6, pediatric pulmonology**
Pre-visit intake, caregiver side. Direction B from `Group7_S2_Ideation.html`.

**Product name: Beforehand.** It appears on the landing screen and in the top bar. "The named ask" remains the name of the mechanism, the short list of specifically named documents, not of the app.

**Audience:** Claude Code. **Deliverable:** one self-contained `.html` file.

> **Everything in this prototype is fictional.** No real patient, no real family, no real clinician data. The child, the appointment, the referral and the documents are invented for demonstration. This must be stated in the menu and on the privacy sheet.

## How to use this document

Sections 5 to 9 are the build spec and are authoritative. Section 6 defines the data structures; build those first and drive everything else from them. Section 15 is the build order, section 16 is the acceptance checklist, and 16.1 is the click path that has to be flawless. Section 17 lists what is deliberately not being built, so do not add it back.

Where this document gives copy in English, that copy goes in the `en` locale. Hebrew is the shipping default: populate `he` with a reasonable first-pass translation and mark every Hebrew string `// TODO: native review`. Do not leave `he` empty and do not fall back to English at runtime.

---

## 1. Problem statement

A pediatric pulmonologist spends 60 to 70 percent of a first visit re-assembling a record that is fragmented exactly where one organisation ends and the next begins, and that is never complete. Four physicians described this independently. The caregiver arrives empty-handed, not from unwillingness but because the only instruction she ever received was "bring whatever you have", which is uninterpretable. She is not short of information. She is short of a specific ask, a channel for the evidence she already holds, and any reason to believe preparing changes anything.

The clinic already tried a generic pre-visit checklist. It lapsed. Published completion for electronic pre-visit questionnaires sits near 50 percent, and some intervention visits ran 6.8 minutes *longer*. A longer form is not the answer, and this prototype must not be one.

## 2. What this prototype is for

It is **not** the test of Direction B. The test is five concierge phone calls to real families. This prototype is the **stimulus** for those calls, and the artifact for the Session 3 share-out: something a caregiver can be handed on a phone, so the conversation is about a real object rather than a description.

That sets the fidelity. It has to click through convincingly on the golden path. It does not have to be robust off it.

## 3. Goals

1. A caregiver goes from link to submitted in under four minutes on the golden path, with no dead end.
2. The **named ask** is immediately legible. A viewer should see at a glance that this asks for specific documents, not "your records".
3. Partial completion is visibly a success state.
4. "I don't know" is demonstrably a first-class answer, and the review screen shows why that helps the clinician.
5. Adaptivity is visible: answers in the questions step change what the documents step asks for.

## 4. Non-goals

| Not building | Why |
|---|---|
| Any clinician-facing screen | Scoped to the caregiver side this sprint |
| Real authentication | The login is faked end to end. See 7.2 and 10.2 |
| Real OCR, real transcription, real translation | Faked. See section 10 |
| Any network call, server or backend | State persists on the device only, with a disclaimer. See 14 |
| Real EHR, health-fund or national-exchange integration | Killed in ideation as un-buildable in a sprint |
| A comprehensive medical history questionnaire | Killed in ideation. The ask is short and per-patient, or it is the thing that already failed |
| A desktop-optimised layout | Phone-first only. Above 700 px the same phone-width app is centred in a frame. See 14 |
| Error handling and recovery states | Out of P0. See 17 |
| Voice input | Out of P0. See 17 |
| The post-visit receipt | Out of P0. See 17 |

---

## 5. The fixture case

All content fictional. Hard-code exactly this into `CASE`.

**Child:** Yotam, age 5.
**Appointment:** Thursday 6 August 2026, 09:20. Pulmonary Institute, floor 3, room 312. Dr. Oren S.
**Referral:** family doctor, for a cough of about four months, worse at night.
**Caregiver:** the mother. Also has an infant. First pulmonology visit.

### 5.1 Document cards

Three base cards, always present. Three conditional cards, each keyed to one answer.

| id | kind | trigger | Title shown | Why it matters (shown on the card) |
|---|---|---|---|---|
| `D1` | paper | base | Discharge letter from Terem urgent care, 14 March 2026 | "It says what they found and what they gave him that night." |
| `D2` | paper | base | Sleep study report, private sleep lab, November 2025 | "Dr. Oren cannot open private clinic results. Only you can bring this one." |
| `D3` | paper | base | Chest X-ray report, private imaging institute, January 2026 | "He can see that it exists. He cannot see the image." |
| `D4` | video | `q5a` = `has_video` | The video you mentioned of Yotam's night cough | "You already filmed the thing he needs to hear." |
| `D5` | paper | `q8a` = `someone_else` | The paper from the emergency room visit you were not at | "You weren't there, so this is the only account of it." |
| `D6` | paper | `q4d` = `yes` | The hospital discharge summary from when he stayed in | "An overnight stay produces the single most useful document." |

**Maximum cards in any one run is five.** `D4` only exists on Branch A and `D6` only exists on Branch D, so they can never both appear. `D5` can appear on any branch.

**"What is this?" explainers**, one per card, plain language. Example for `D2`: "A sleep study is an overnight test that records breathing while a child sleeps. If Yotam had one at a private clinic, you would have been given a report, usually two or three pages."

---

## 6. Data model

Build these three objects first. Everything else renders from them. **No user-facing string appears in markup.**

### 6.1 `STRINGS`

Interface chrome only: buttons, field labels, headings, loader text, helper copy.

```js
const STRINGS = {
  en: { continue: "Continue", skip: "Skip this", dontKnow: "I don't know", /* ... */ },
  he: { continue: "המשך", /* TODO: native review */ }
};
```

### 6.2 `CASE`

The fixture: child, appointment, question tree, option lists, document cards. Every text field inside `CASE` is itself locale-keyed.

```js
const QUESTION = {
  id: "q4a",
  type: "bucketed",              // single | multi | bucketed | scale | approx_date | open_text
  branch: "A",                   // "A" | "B" | "C" | "D" | null  (null = asked on every path)
  screen: true,                  // true = own screen; false = inline reveal on its parent's screen
  parent: null,                  // question id, required when screen === false
  showIf: null,                  // { questionId, in: [optionId, ...] }, required when screen === false
  text: { en: "...", he: "..." },
  help: null,                    // optional line under the question
  options: [                     // omitted for scale, approx_date, open_text
    { id: "none", text: { en: "None", he: "..." } },
    { id: "gt10", text: { en: "More than 10", he: "..." } }
  ],
  exclusiveOptions: ["unknown"], // for multi: selecting these clears and disables the rest
  unknown: true,                 // render the "I don't know" option
  confidence: true,              // render the Sure / Roughly / Guessing control
  scale: { min: 0, max: 5, minLabel: {...}, maxLabel: {...} }   // type "scale" only
};

const CARD = {
  id: "D4",
  kind: "video",                 // "paper" | "video"
  base: false,
  trigger: { questionId: "q5a", optionId: "has_video" },   // null when base === true
  title:  { en: "...", he: "..." },
  date:   { en: "2am, last winter", he: "..." },   // shown under the title; null where unknown
  source: { en: "Your phone", he: "..." },
  why:     { en: "...", he: "..." },
  explain: { en: "...", he: "..." },
  origin:  { en: "Added because you told us about the video", he: "..." },  // null when base
  read: null   // paper cards only. See 7.8
};
```

### 6.3 `STATE`

```js
const STATE = {
  locale: "he",
  loggedIn: false,
  phone: "",
  respondent: null,        // "mother" | "father" | "grandparent" | "other"
  branch: null,            // "A" | "B" | "C" | "D" | "other" | null
  answers: {},             // questionId -> Answer.  A missing key means never reached.
  cards: {},               // cardId -> CardState
  note: "",
  submitted: false,
  rescheduledTo: null,     // slot id
  screen: "landing"
};

// Answer
{
  status: "answered" | "unknown" | "skipped",
  value: null,             // optionId | [optionId] | number | {month, year} | string. null unless answered.
  detail: null,            // free text captured by an option that carries detail: "open_text"
  confidence: null,        // "sure" | "roughly" | "guessing" | null
  secondHand: false        // set true on q8 when q8a === "someone_else"
}

// CardState
{
  status: "untouched" | "attached" | "will_bring" | "will_get" | "cannot_get",
  files: [],               // { name, kind, objectUrl }
  extracted: null,         // shape mirrors CARD.read. See 7.8
  opened: false            // unused in P0. Reserved so the receipt can be added later. See 17.
}
```

**Rules that follow from this model, and must be implemented:**

- `answered`, `unknown`, `skipped` and *missing* are four distinct things. Never collapse them.
- **`STATE.branch` is derived from `q1`.** `cough`→A, `noisy`→B, `breathless`→C, `infections`→D, `other`→`"other"`. If `q1` is `unknown` **or skipped**, branch is `null`. Branch `"other"` and branch `null` both go straight from `q2` to the common tail.
- **Card presence is derived, never stored.** A conditional card exists if and only if its trigger matches `STATE.answers` right now. If the triggering answer changes, or its branch is abandoned, the card disappears and its `CardState` is discarded.
- **Only a change to `q1` clears answers.** On a `q1` change, delete every answer whose question has a non-null `branch` other than the new one, then re-derive the cards. Navigating back and forward through a branch without changing `q1` never destroys anything.
- **`showIf` matching.** `{ questionId, in: [...] }` is true when the target answer has `status: "answered"` and its value, or **any** member of its value if the target is `multi`, appears in `in`. An `unknown` or `skipped` target never satisfies a `showIf`.
- **`showIf` is allowed on `screen: true` questions.** `q5a` is one: it is a full screen that is only shown on some paths. `parent` is required only when `screen` is `false`.
- **An option may carry `detail: "open_text"`.** Selecting it reveals a text field in place, written to `Answer.detail`. It is part of the parent answer: it is never its own question, never its own progress segment, and never counted separately on review.
- **Every `scale` question** renders its two anchor labels and a separate "I don't know" chip beside the track, since a scale has no option list to hold one.
- The open "anything else" slot on the documents screen has id `DX`, kind `paper`, no title, no trigger and no `read` fixture. It is always present, it is never counted in the header number, and its attachments do count in the review document totals.

---

## 7. Screens

Twelve screens plus a menu and one sheet. Order is deliberate: **quick wins first**. Questions come before documents because tapping answers builds momentum, and hunting for a March discharge letter does not.

```
[0] Landing
     ↓
[L] Log in            phone number, then one-time code        faked, see 7.2
     ↓
[1] Who is answering                                          one question, ~20 seconds
     ↓
[Q] Anamnesis         6 to 9 question screens, branching      see section 9
     ↓
[D] Documents         the named ask, 3 to 5 cards + open slot
     ↓   ↘  [R] Reschedule       escape hatch, also in the menu
[C] Note              free text, optional
     ↓
[V] Review
     ↓
[S] Sent
```

**Top bar** with back, screen title and menu button on every screen except `[0]`, `[L.1]` and `[L.2]`, which have no menu and no back. `[R]` has a back that returns to whichever screen opened it.

**Menu** is reachable from `[0]` (as "What is this?" plus a language control) and from every screen that has a top bar, so language can be changed from anywhere.

**Sticky bottom bar** with the progress bar and **"Send what I have"** on `[1]` through `[V]`. Enabled from `[1]` onward, never disabled.

### 7.1 `[0]` Landing

- **Beforehand**, small, at the top. The product name appears here and in the top bar, nowhere else.
- "Yotam's appointment", Thursday 6 August, 09:20, Pulmonary Institute, Dr. Oren S.
- One line placing the entry: "You got here from the text message about Yotam's appointment."
- The promise, prominent: **"Dr. Oren reads this before you walk in."** This is the reciprocity condition and the reason anyone finishes the form.
- "About 4 minutes. You can stop and come back."
- What makes it different: "We are only asking for what your file could not tell us."
- Primary: **Start**. Secondary: **What is this?** opens the privacy sheet (7.11).

### 7.2 `[L]` Log in

The only gate in the product, and it must not feel like one. No password, no account, no email. The caregiver already receives clinic messages on that number.

**`[L.1]` Phone number.** An instruction above the field, phrased as a command: "Enter the mobile number the clinic texts you on." One numeric field formatted for an Israeli mobile; its label lives on for screen readers only. Continue is **never disabled**: tapping it with an implausible number shows an amber inline error ("The number should start with 05 and have 10 digits.") in a **fixed-height line under the field**, so the button never jumps, and the error clears by itself the moment the number is right. This is the one deliberate exception to section 17's "no error states". The language switch sits bottom-centre, labelled as an action in the target language ("Switch to English" / "מעבר לעברית"), on both login screens.

**`[L.2]` One-time code.** Everything centre-aligned. Four boxes, auto-advancing, auto-focus on the first. Above: "We sent a code to 05X-XXXXXXX". Below: "Didn't get it? Send again", which starts a 30 second countdown and does nothing else.

Faked: **any four digits are accepted** after a 1 s "Checking..." state. A small demo note on the screen says so. Once `STATE.loggedIn` is true a resumed session skips this screen.

### 7.3 `[1]` Who is answering

One `single` question, `id: "respondent"`: Mother / Father / Grandparent / Another guardian.

It is not decoration. It is shown on review, and it selects the copy variant on the `q8a` follow-up (7.5).

There is no language step. The app boots Hebrew and RTL. English lives in the menu.

### 7.4 `[Q]` Anamnesis, screen behaviour

The tree itself is section 9. This is how a question screen behaves.

- **One `screen: true` question per screen.** Inline reveals appear underneath their parent on the same screen, animated in, and disappear when the parent answer changes.
- **"I don't know"** renders as a full-width option in the same visual weight as the others, at the bottom of the option list. It sets `status: "unknown"`.
- **"Skip this"** is a text button under the options on every question screen. It sets `status: "skipped"` and advances. This is the only input for the "passed on" counter.
- **Confidence** renders under the answer when `confidence: true`, as three chips: Sure / Roughly / Guessing. Optional, default unset, does not block Continue.
- Continue is enabled once the question has any status, including `unknown` and `skipped`.
- Back returns to the previous screen on the current path and leaves answers intact, except when `q1` changes (see 6.3).

### 7.5 The `q8a` copy variant

When `q8a` is answered `someone_else`, set `secondHand: true` on `q8` and show one line, chosen by `STATE.respondent`:

- Mother or Father: "That is useful to know. Dr. Oren will check that one himself."
- Grandparent or Another guardian: "That is useful to know. If Yotam's parent was there, Dr. Oren may ask them too."

### 7.6 `[D]` Documents, the named ask

The most important screen in the build. It must not read as an upload box.

**Header:** `"{n} things Dr. Oren cannot get himself"`, where `n` is the derived card count as a **numeral**, never spelled as a word, since a spelled number needs gender agreement in Hebrew. `n` is computed on entry, and because every question precedes this screen it does not change while the caregiver is on it.
**Subhead:** "These are the only ones missing. Everything else he already has."

One card per derived document, in id order, each showing its title, its date and source, and its `why` line. A conditional card carries a one-line origin note: "Added because you told us about the video." Not a toast, since she may reach this screen minutes later.

**Actions by card kind:**

- `paper`: Find it on my phone · Take a photo · I don't have it · What is this?
- `video`: Find it on my phone · I don't have it any more · What is this?
  A video is already in her camera roll, so there is no capture step and no scan.

**Find it on my phone** opens the real system file picker, renders a real local thumbnail, and sets `attached`. Nothing is uploaded.

**Take a photo** goes to `[D.1]`.

**I don't have it** never scolds. It opens three follow-ups:

| Choice | Sets |
|---|---|
| "I have it, I'll bring it on the day" | `will_bring` |
| "I can get it before Thursday" | `will_get` |
| "I can't get it" | `cannot_get`, and offers **"Would it help to move the appointment?"** inline, with two buttons: **"Move my appointment"** goes to `[R]`, **"No, I'll come anyway"** dismisses the offer and leaves the card at `cannot_get` |

**What is this?** opens the card's `explain` sheet.

**At the bottom:** the open slot `DX`, "Anything else you think matters?" It comes last on purpose. The named items are the hypothesis; the open slot is the safety net.

### 7.7 `[D.1]` Capture instructions

One screen before the camera, because this is where a photo becomes unusable.

- Put the page on a flat surface.
- Get all four corners in the frame.
- No flash on shiny paper.
- One page at a time.

Then a camera view with a frame guide and a shutter. Use `getUserMedia` where available and permitted; otherwise fall back silently to the file picker labelled "Choose a photo". Never dead-end.

### 7.8 `[D.2]` Read and correct

After capture, 1.5 s of "Reading the document...", then a result card labelled **"Read automatically. Please check."** showing four fields, populated from that card's `read` fixture.

For `D1`:

| Field | Value | State |
|---|---|---|
| Document type | Discharge letter | confident |
| Date | 14 March 2026 | confident |
| Place | Terem urgent care | confident |
| Child's name | Yotam | **flagged: "We're not sure we read this correctly"** |

Every `paper` card carries its own `read` fixture in `CASE`, matching its own title and source. `uncertain` is always `"childName"`, so the correction moment exists on every card. `DX` has no fixture: it reads as document type "Not sure", everything else blank, all four fields flagged, and the user fills them in.

**Completing `[D.2]` sets that card to `attached` and returns to `[D]`.** Backing out of `[D.1]` or `[D.2]` without shooting leaves the card `untouched`.

Every field is editable and written back to `CardState.extracted`. The flagged field is the point of the interaction: it shows that machine output is correctable and that the system says where it is unsure rather than presenting fluent output as fact. **Do not remove it to make the demo look cleaner.**

### 7.9 `[C]` Note

One free-text box: "Is there anything you want Dr. Oren to know before you come in?" Optional, and the bottom bar makes leaving it empty obviously fine.

### 7.10 `[V]` Review

- Six sections, each holding fixed questions. Anything never reached is omitted, and an empty section is not rendered.

| Section | Holds |
|---|---|
| About Yotam | `respondent` |
| What is happening | `q1`, `q2`, and every branch question `q3*` to `q5*` |
| Medicines | `q6`, `q6_which`, `q6_helps` |
| History | `q7`, `q8`, `q8a` |
| Documents | every derived card and `DX`, with its status and, where present, its corrected `extracted` fields |
| Your note | `q9` and `STATE.note` |
- Every row tappable, jumping back to its question and returning to review with state preserved.
- **Second-hand tag** on any answer with `secondHand: true`.
- **Confidence in words** where set. All three render: "Sure", "Roughly", "Guessing".
- **Gaps panel, two counters kept separate:**
  - *Don't knows:* "You told us you don't know N things. That is useful. Dr. Oren now knows exactly where to check." Listed by name.
  - *Passed on:* "You passed on M questions." Listed, each tappable to answer now.
  - Never-reached questions appear in neither and are not shown.
  - **A counter at zero is not rendered at all**, neither its sentence nor its list. If both are zero the whole gaps panel is absent.
- **Summary line, computed at runtime, never hard-coded.** Counting rules, so two builds agree:
  - *Answers* = questions with `status: "answered"`. Inline reveals count individually. `unknown` is not an answer.
  - *Documents* = cards with `status: "attached"`, split by `kind`, including `DX`.
  - Rendered "N answers · P documents · V videos · K don't knows · M passed on". **Any zero term is dropped from the line rather than printed as "0".**
- Primary: **Send to Dr. Oren**.

### 7.11 The privacy sheet

Reachable from `[0]` and the menu. Plain language, one short sheet:

- This is a prototype. Nothing here is a real medical record.
- "Right now everything you enter stays on this phone, in this browser. Nothing is sent anywhere."
- "In the real version this would be stored securely in the clinic's system and seen only by Yotam's care team."
- "Your photos are not uploaded. They stay on your device."
- Nothing here is a diagnosis, and no machine draws a clinical conclusion.

### 7.12 `[S]` Sent

- "Sent. Dr. Oren will read this before Thursday morning."
- **What you still need to bring:** every card in `will_bring` or `will_get`, by name. If there are none, say so plainly rather than showing an empty heading.
- Appointment details again. "Add to calendar" shows a confirmation toast and does nothing else.
- Secondary: **Change my appointment** goes to `[R]`.

### 7.13 `[R]` Reschedule

Reachable from `[D]`, from `[S]` and from the menu.

- Framed as "Would more time help?", not "Cancel".
- Three fictional slots, one of them the following week.
- Confirming sets `STATE.rescheduledTo` and states explicitly: **"Your answers are saved. The documents we asked for stay the same."**

### 7.14 `[Menu]`

Slide-over sheet from the top bar:

- **Language**: עברית / English, with the fake loader. Hebrew is the default.
- **Save and continue later**
- **Change my appointment**
- **How we handle this information** (7.11)
- **Restart demo**, labelled as a demo affordance. Clears `STATE` and returns to `[0]`.

### 7.15 The progress bar

Segments, not a percentage. The denominator is:

```
1 ([1])  +  number of screen:true questions on the current path  +  1 ([D])  +  1 ([C])  +  1 ([V])
```

- Inline reveals are never segments.
- Fill is driven by **position**, not by how many questions were answered, so skipping does not make the bar lie.
- The denominator is unknown until `q1` has **any** status, including `unknown` and `skipped`. Until then show the `[1]` segment filled and the rest as one indeterminate block.
- Recompute on any `q1` change and on any `q3a` change. When the total grows, never un-fill a segment already passed.
- `aria-live="polite"` on the count.

---

## 8. Screens to build, checklist

`[0]` · `[L.1]` · `[L.2]` · `[1]` · `[Q]` (the question screen, rendered 6 to 9 times) · `[D]` · `[D.1]` · `[D.2]` · `[C]` · `[V]` · `[S]` · `[R]`, plus `[Menu]` and the privacy sheet.

`[L]` is the pair `[L.1]` and `[L.2]`, and is referred to as `[L]` where the distinction does not matter.

---

## 9. The question tree

**Hard cap: no path exceeds nine `screen: true` questions.** If a change would push a path past nine, cut the question rather than the cap.

`respondent` on `[1]` is not counted in the nine.

### Root, asked on every path

**`q1` · `single` · branch `null`**
"What is the main reason for Yotam's visit?"

| optionId | Label | Routes to |
|---|---|---|
| `cough` | A cough that will not go away | Branch A |
| `noisy` | Noisy breathing or wheezing | Branch B |
| `breathless` | He gets out of breath easily | Branch C |
| `infections` | Chest infections that keep coming back | Branch D |
| `other` | Something else (`detail: "open_text"`) | common tail |
| `unknown` | I don't know | common tail |

**`q2` · `approx_date` · branch `null` · confidence**
"Roughly when did it start?" Month and year pickers, no day. Shortcut chips above: `last_month` In the last month · `lt_year` Less than a year ago · `gt_year` More than a year ago · `unknown` I don't know. A chip fills the pickers, except `unknown`, which sets `status: "unknown"` and leaves them empty.

`q2` is asked on **every** path, including `other`, `unknown` and a skipped `q1`.

### Branch A, cough

**`q3a` · `multi` · exclusive `no_pattern`, `unknown`**
"When is the cough worst?"
`at_night` At night · `early_am` Early morning · `exertion` During or after running · `cold_air` In cold air · `after_cold` After a cold · `no_pattern` No pattern I can see · `unknown` I don't know

**`q4a` · `bucketed` · confidence**
"In the last month, how many nights did the cough wake him?"
`none` None · `1to3` 1 to 3 · `4to10` 4 to 10 · `gt10` More than 10 · `unknown` I don't know
→ **`q4a_wheezy` · `single` · inline · parent `q4a` · showIf `q4a` in [`4to10`, `gt10`]**
"On those nights, did he also sound wheezy or short of breath?" `yes` Yes · `no` No · `unknown` I don't know

**`q5a` · `single` · screen · showIf `q3a` in [`at_night`]**
"Have you ever filmed or recorded it?"
`has_video` Yes, I have a video · `could_film` No, but I could film it · `no` No · `unknown` I don't know
→ `has_video` derives card **`D4`**.

### Branch B, noisy breathing

**`q3b` · `single`** "What does it sound like?"
`whistle` Whistling · `rattle` Rattling or bubbling · `bark` A bark · `hard` Hard to describe (`detail: "open_text"`) · `unknown` I don't know

**`q4b` · `bucketed` · confidence** "How often in the last month?"
`not_this_month` Not in the last month · `few` A few times · `most_weeks` Most weeks · `most_days` Most days · `unknown` I don't know

**`q5b` · `scale` 0 to 5** "How much does it stop him doing things?" Anchors "Not at all" and "A lot".

### Branch C, breathless

**`q3c` · `multi` · exclusive `unknown`** "When does it happen?"
`sport` Running or sport · `stairs` Stairs or uphill · `at_rest` At rest · `when_ill` Only when he is unwell · `unknown` I don't know

**`q4c` · `single`** "Does he keep up with other children his age?"
`yes` Yes · `mostly` Mostly · `stops_sooner` No, he stops sooner · `unknown` I don't know

**`q5c` · `scale` 0 to 5** "How much does it stop him doing things?" Anchors "Not at all" and "A lot".

### Branch D, repeat infections

**`q3d` · `bucketed` · confidence** "How many chest infections in the last 12 months?"
`one` 1 · `2to3` 2 to 3 · `gte4` 4 or more · `unknown` I don't know
→ **`q3d_abx` · `single` · inline · parent `q3d` · showIf `q3d` in [`2to3`, `gte4`]**
"Did any of them need antibiotics?" `most` Yes, most · `some` Yes, some · `no` No · `unknown` I don't know

**`q4d` · `single`** "Was he ever kept in hospital overnight for his breathing?"
`yes` Yes · `no` No · `unknown` I don't know
→ `yes` derives card **`D6`**.

### Common tail, every path

**`q6` · `single`** "Is he taking any inhaler or breathing medicine?"
`daily` Yes, every day · `prn` Yes, only when he needs it · `stopped` He tried one and stopped · `no` No · `unknown` I don't know
→ **`q6_which` · `multi` · inline · parent `q6` · showIf `q6` in [`daily`, `prn`, `stopped`]**
"Which ones?" `inh_a` `inh_b` `inh_c` `inh_d`, four plausible fictional inhaler names, plus `other` Other (`detail: "open_text"`), plus `unknown` "I don't remember the name". Exclusive: `unknown`.
→ **`q6_helps` · `scale` 0 to 5 · inline · parent `q6` · same showIf**
"Does it help?" Anchors "Not at all" and "A lot".

**`q7` · `multi` · exclusive `none`, `unknown`** "Is there anything he reacts to?"
`dust` Dust · `animals` Animals · `pollen` Pollen or seasons · `cold_air` Cold air · `exercise` Exercise · `smoke` Cigarette smoke · `none` Nothing we have noticed · `unknown` I don't know
Helper line: *"Only tick what you have actually seen happen."* This guards against the CAMP finding that most reported triggers are not borne out.

**`q8` · `single`** "Has he been to an emergency room or urgent care for his breathing?"
`never` Never · `once` Once · `2to3` 2 to 3 times · `gt3` More than 3 times · `unknown` I don't know
→ **`q8a` · `single` · inline · parent `q8` · showIf `q8` in [`once`, `2to3`, `gt3`]**. Not on `never` and **not on `unknown`**, because "I don't know" is never treated as affirmative.
"Were you there each time?" `yes` Yes, every time · `someone_else` No, someone else took him at least once · `unknown` I don't know
→ `someone_else` derives card **`D5`** and sets `secondHand` on `q8`. Copy variant per 7.5.

**`q9` · `open_text` · optional** "Anything else you have noticed that we have not asked about?"
This is the one question with no "I don't know". It carries `nothing` **"Nothing comes to mind"** instead, stored as a normal answered value. Blank and never-visited stay distinct from it.

### Every question also carries

- `unknown: true` on all of the above except `q9`, which uses `nothing` in its place.
- `confidence: true` only on `q2`, `q4a`, `q4b`, `q3d`.
- Skip on every `screen: true` question, per 7.4.

### Path audit

Build the progress denominator from this table, not from a guess.

| Path | `screen:true` questions | Sequence |
|---|---|---|
| A with `at_night` ticked | **9** | q1 q2 q3a q4a q5a q6 q7 q8 q9 |
| A without `at_night` | 8 | q5a not shown |
| B | **9** | q1 q2 q3b q4b q5b q6 q7 q8 q9 |
| C | **9** | q1 q2 q3c q4c q5c q6 q7 q8 q9 |
| D | 8 | q1 q2 q3d q4d q6 q7 q8 q9 |
| `other`, `unknown`, or skipped at root | 6 | q1 q2 q6 q7 q8 q9 |

The cap holds on every path.

---

## 10. What is faked, and how it must behave

Faked does not mean absent. Each of these needs a visible, believable behaviour.

**10.1 Document reading.** 1.5 s delay, then structured fields with one field flagged uncertain. Always labelled "Read automatically". Always editable.

**10.2 Login.** Any plausible phone number. Any four digits, after a 1 s "Checking...". Resend runs a 30 s countdown and does nothing.

**10.3 Language switching.** 1.2 s loader, then a full re-render from `STRINGS` and `CASE` at the other locale key, plus a real `dir` flip on the document root. Not a text swap alone.

**10.4 Submission.** No network. A short pending state, then `[S]`.

**10.5 The named items.** Fixed content in `CASE`, presented as if derived from the referral letter and from what the clinic record could not reach.

**10.6 Appointment slots, calendar add, the SMS itself.** The three slots are fixed content rather than fetched, but **choosing one is a real state change**: it sets `STATE.rescheduledTo` and `[S]` shows the new date. "Add to calendar" and the SMS are inert.

## 11. What actually works

| Behaviour | Requirement |
|---|---|
| Navigation | Forward and back through every screen, without losing answers. Only a change to `q1` clears a branch, and it re-derives the cards |
| Branching | `q1` genuinely routes. Inline reveals genuinely appear and disappear |
| Cross-step adaptivity | `q5a`, `q4d` and `q8a` genuinely derive `D4`, `D6` and `D5` |
| Four answer states | answered, unknown, skipped and never-reached, all four distinct in `STATE`. The first three surface on review; never-reached is omitted |
| Confidence | Stored per answer, rendered in words on review |
| Skip | A real control on every question screen, feeding the passed-on counter |
| Progress | Segments per 7.15. Never claims completion when things were skipped |
| Send what I have | Enabled from `[1]`, always reaches `[V]`, never blocked |
| File picker | Real, with a real local thumbnail. No upload |
| Camera | Real `getUserMedia` where available, silent fallback to the picker |
| Review edit | Real jump-back-and-return with state preserved |
| Language | Real full re-render and real RTL flip. Hebrew is the boot state |
| Save and resume | `localStorage` inside `try/catch`, falling back to in-memory. Includes `loggedIn`. Never throws |
| Reschedule | Real state change, reflected on `[S]` |
| Counts | Computed from `STATE` at render time |

## 12. Guardrails, pass or fail

A build that violates one of these is wrong, not merely unpolished.

1. **No real patient data anywhere.** Everything fictional, and labelled fictional in the menu and on the privacy sheet.
2. **The app never concludes.** No screen tells the caregiver what Yotam has, what is wrong, or what to do. It collects and routes. Nothing more.
3. **Machine output is labelled and correctable.** The document read, every time.
4. **Uncertainty is surfaced, never smoothed.** "I don't know" is a value, confidence is captured, and the read admits where it is unsure.
5. **No dark patterns on completion.** No red, no "incomplete", no guilt copy, no blocking. Partial is a success state.

## 13. Visual direction

**The intake is a conversation with the clinic, rendered as a messenger chat — "WhatsApp, but blue."** Chosen by the team over seven design rounds; the committed spec is `design-chat-final.html` (exploration history in `design-explorations.html` and `design-chat-explorations.html`), recorded durably in `previsit-design.md`. This supersedes the earlier low-fi wireframe direction.

- **The chat frame.** A deep-blue header (`#24518F`) carries the clinic's identity: the Gordon logo in a white circle avatar, "מרפאת ריאות ילדים גורדון", "ד״ר אורן שגב · לפני הביקור", and a kebab menu icon. The conversation sits on a blue-tinted dotted wallpaper.
- **Two voices.** Clinic messages are white bubbles with the sharp corner turned toward the clinic's mini logo avatar; the caregiver's answers are light-blue bubbles with a generic person mark. Corner direction uses logical properties so it flips correctly between RTL and LTR. Emphasis inside a bubble (the appointment, the send summary) is a raised light-blue card, never a bare field.
- **The conversation accumulates.** Every answered question stays in the stream as a sent message; a one-time pencil hint says answers are tappable. Tapping one enters a focused edit mode — the rest of the conversation hides until "הבא" confirms or "ביטול" escapes without changes. This is the back navigation; there is no back button on chat screens.
- **Controls are quick replies.** Options render as pill buttons, selected = solid blue with a check; unselected wear a thin light border. "I don't know" is a pill of the same size and weight as any answer.
- **The composer.** A continuous, textless progress bar (position-driven, filling from the right in Hebrew, one step pre-filled from the first question) sits above one action row: "דילוג על השאלה" on one side, the "הבא" pill with an arrow on the other. The step count survives as visually-hidden `aria-live` text. The solid paper-plane **"שלח"** appears only on the final screen, facing the sending direction — nothing leaves the phone before that button. The landing has no composer; its primary is a full-width "בואו נתחיל" quick reply with a borderless "מה זה?" beneath.
- **Motion.** Entrances only, transform and opacity only, nothing over 250ms, and gated to real transitions — intra-screen re-renders never replay. The clinic "types" (~500ms of pulsing dots, composer disabled) before each next message; new bubbles rise in, the just-sent answer pops, landing bubbles stagger, the progress bar grows via scaleX, the menu and sheets slide, and on שלח the plane flies off the button before the sending state. All of it collapses under `prefers-reduced-motion`. No spinners, no confetti: sending reads as relief, not victory.
- One accent family (the blues) plus the logo's green; no red anywhere. System font stack, rounded cards, 999px pills, one soft shadow level. Icons are inline SVG stroked in `currentColor`. Capture, read-and-correct and reschedule render as focused white panels with a back link; review is the conversation itself plus a gaps bubble and a send-summary card.

## 14. Technical constraints

- **One self-contained `.html` file.** Inline CSS and JS. No build step, no CDN, no framework, no network at runtime.
- **Phone-first.** Design at 390 × 844. Above 700 px viewport width, render the app inside a centred phone frame on a plain ground, so it reads correctly on a laptop and a projector.
- **Storage:** `localStorage` wrapped in `try/catch` with an in-memory fallback, so the demo survives `file://` restrictions.
- **RTL is structural, not a stylesheet afterthought.** Build it in from the first commit.
- **Accessibility floor:** every control keyboard reachable and operable, visible focus ring, text contrast at least 4.5:1, real labels on every input, `aria-live` on the progress count and the fake loaders. Colour never the only carrier of state.

## 15. Build order

1. Shell: `STATE`, `STRINGS`, `CASE`, router, top bar, sticky bottom bar, Hebrew and RTL from the start.
2. `[0]` Landing and the privacy sheet.
3. `[L.1]` and `[L.2]`, faked.
4. `[1]`, and the question engine driven by `CASE`, with all six input types, the `unknown` option, the confidence control and Skip.
5. The tree and branching, including inline reveals and the branch-clearing rule.
6. `[D]`, card derivation, the five card states, and the open slot.
7. `[D.1]` and `[D.2]`, capture and correction.
8. `[C]`, then `[V]` with edit-and-return and the two gap counters.
9. `[S]` and `[R]`.
10. `[Menu]`, the English locale and the language switch.
11. Save and resume, including the logged-in session.
12. "Send what I have" from every screen, the progress bar per 7.15, and the accessibility floor.

## 16. Acceptance criteria

The prototype is done when someone handed a phone can do all of this unaided.

- [ ] Complete the click path in section 16.1 in under four minutes with no dead end.
- [ ] Log in with any phone number and any four digits, and land on `[1]`.
- [ ] Confirm the app boots in Hebrew and RTL. Switch to English from any screen, watch layout, text and progress all follow, then switch back.
- [ ] Answer `q1` "A cough that will not go away", then "I don't know" at every subsequent question that offers it, and "Nothing comes to mind" at `q9`. Reach review and send. Review lists every one of them.
- [ ] Answer `q1` "Noisy breathing or wheezing", then Skip every subsequent question. Review shows them all under "passed on", and the don't-knows sentence and term are **absent entirely rather than printed as 0**.
- [ ] Reach review from `[1]` via "Send what I have". Review shows the respondent answer, no invented questions, and sending is allowed.
- [ ] Go back from a Branch A question, change `q1` to `infections`, and confirm Branch A's answers are gone, `D4` has disappeared, and the progress denominator has recomputed without un-filling a passed segment.
- [ ] Answer `q5a` "Yes, I have a video", reach `[D]`, and see a fourth card with its origin note.
- [ ] Photograph a document, correct the flagged name field, reach review, and see the corrected value.
- [ ] Mark one card "I have it, I'll bring it on the day", send, and see it named on `[S]`.
- [ ] Reschedule from `[D]` and be told on screen that answers are kept.
- [ ] Leave, reload the page, and resume past the login at the same screen.
- [ ] Tab through an entire question screen, including the confidence chips and Skip, using only the keyboard.

### 16.1 The demo click path

This exact sequence must be flawless. Everything else can be rough. Copy is quoted in English for legibility; the run can be done in either locale.

1. `[0]` → Start
2. `[L]` any phone number → any four digits → "Checking..." → in
3. `[1]` Mother
4. `q1` "A cough that will not go away"
5. `q2` "Less than a year ago", confidence "Roughly"
6. `q3a` "At night" and "After a cold"
7. `q4a` "More than 10", confidence "Sure" → inline `q4a_wheezy` "Yes"
8. `q5a` "Yes, I have a video" → **`D4` will appear**
9. `q6` "He tried one and stopped" → `q6_which` name one → `q6_helps` 2
10. `q7` "Dust", "Cold air"
11. `q8` "2 to 3 times" → `q8a` "No, someone else took him at least once" → **`D5` will appear**
12. `q9` Skip
13. `[D]` header shows the numeral 5. Copy is `"{n} things Dr. Oren cannot get himself"` with `n` as a numeral in both locales, never spelled as a word
14. `D1` → Take a photo → `[D.1]` instructions → shutter → `[D.2]` read → correct the flagged name field
15. `D2` → I don't have it → "I can't get it" → **decline the reschedule offer**
16. `D3` → Find it on my phone
17. `D4` → Find it on my phone
18. `D5` → I don't have it → **"I have it, I'll bring it on the day"**
19. `[C]` skip
20. `[V]` show the gaps panel, the second-hand tag and the confidence words. Tap one answer, change it, return.
21. Send → `[S]`, which names `D5` as the one thing still to bring.

Roughly 90 seconds at demo pace.

## 17. Held out of P0, deliberately

Not cut for lack of value. Cut so the P0 build lands.

**The post-visit receipt.** A screen after the visit showing which of the caregiver's items the clinician actually opened and what changed as a result. Concept 14, and the reciprocity mechanism behind insight I4: the reason a second form ever gets filled. Out because it demonstrates nothing about the intake flow itself. `CardState.opened` exists in the model so this can be added without a rewrite.

**Voice input.** Concept 12. Removes the literacy barrier, the language barrier and the typing barrier at once, and is the highest-value P1 item for a Hebrew-speaking clinic. Out because a convincing fake needs a recorder, a waveform, a timer and a correction pass: a screen's work for one optional question.

**Error and recovery states.** Wrong code, expired code, unreadable photo, unsupported file type, offline. Out entirely. Fail soft and silently rather than spending effort on messages nobody reads in a demo.

**Real authentication and real camera access.** The login is faked end to end. Camera falls back to the file picker wherever `getUserMedia` is unavailable, and that fallback is an acceptable P0 outcome rather than a degradation.

---

## Appendix A: traceability

Every feature traces to the team's own synthesis or ideation. Anything not in this table should be challenged.

| Feature | Source |
|---|---|
| Specifically named documents | Concept 7, the named ask · I3 · I4 |
| Derived from what the record could not reach | Concept 6, Boundary Map |
| Two countable, recent questions | Concept 8, Two Questions · the nurse's minimum form |
| "I don't know" as a recorded value | Concept 9, Don't-Know Button |
| Confidence on recall answers | Concept 10, Confidence Dial · I5 |
| The night-cough video channel | Concept 13, Cough Album |
| "Were you there?" second-hand tagging | Concept 19, Stand-in Page · the grandmother ER gap |
| Plain-language "What is this?" explainers | Concept 16, Corridor Card |
| Short and per-patient, not comprehensive | The killed concept, "a comprehensive family questionnaire" |
| No conclusions, correctable machine output | I2 · guardrails, human in the loop |
| Trigger question warning copy | Desk research, CAMP n=1,041, 39% |
| Partial completion as a success state | Desk research, ~50% completion, +6.8 min visits |
| Phone number plus one-time code as the only gate | Not from the research. A product decision: the lightest credential a hospital would accept and one a caregiver cannot forget |
| Reschedule as an escape hatch off the document step | Not from the research. A product decision: converts a family arriving empty-handed into a visit that works |
| The post-visit receipt (P1, see 17) | Concept 14 · I4, reciprocal not motivational |
