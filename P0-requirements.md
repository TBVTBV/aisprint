# P0 must-have requirements

**Pre-visit intake, caregiver-side prototype**
Group 7 · AI Product Sprint 2026 · Challenge #6, pediatric pulmonology
Direction B, "The Named Ask"

Cut any of these and the prototype stops making its argument. Full detail, screen specs and acceptance criteria live in `PRD.md`. Flow diagram in `task-flow.svg`.

---

## Access

**1. No account creation.** Entry is a link. The only gate is a phone number plus a one-time code, faked in the prototype so that any number and any code are accepted.

**2. The session persists.** A returning caregiver lands where they left off rather than back at the gate.

## The named ask

**3. Documents are specifically named.** Each item carries a name, a date and a source. Never a generic upload box. This is the whole hypothesis and the one thing that separates this from the checklist the clinic already tried.

**4. Each item says why the clinician needs it,** in one plain line.

**5. At least one item is added at runtime** by an earlier answer, and says on the card why it appeared.

**6. "I don't have it" is a normal outcome** with its own follow-up. Not a failure state, no scolding copy.

**7. Attaching works two ways:** choosing a file from the phone, and photographing a page, with capture instructions shown before the camera opens.

**8. Anything the app extracts from a document is labelled as machine-read, flagged where it is unsure, and editable.** At least one field must demonstrate the uncertain state. Do not remove it to make the demo look cleaner.

## The question engine

**9. Questions are data-driven and progressively disclosed.** The tree decides what comes next from what has already been answered.

**10. Up to nine questions on any single path.** Never more.

**11. Follow-ups reveal inline** under their parent question, never as a new screen.

**12. Every question carries an explicit "I don't know",** stored as a value that is distinct from skipped and from unanswered.

**13. Recall questions carry a confidence marker,** shown in words on the review screen.

**14. Six input types work:** single select, multi select, bucketed ranges, scale, approximate date, free text.

## Completion and honesty

**15. Submit is available from the second step onward and is never disabled.** A partial form reaches review and sends.

**16. Review shows gaps as two separate counters,** don't knows and passed on, framed as useful information for the clinician rather than as omissions.

**17. All counts on review are computed at runtime,** never hard-coded.

**18. Review rows are tappable to edit** and return to review afterwards.

**19. The app never states a conclusion about the patient.** It collects and routes. Nothing more.

**20. Fictional-data notice and the local-storage disclaimer are both present.**

## Mechanics

**21. Phone-first layout,** shown inside a device frame on wider viewports so it demos correctly on a laptop and a projector.

**22. Hebrew by default, with full RTL.** English available from the menu, switchable from any screen without losing state.

**23. Save, close, reopen and resume** where the caregiver left off.

**24. Reschedule** reachable from the document step and from the menu, stating on screen that answers are kept and the named list stays the same.

**25. Single self-contained HTML file.** No build step, no CDN, no network at runtime, no dead ends on the happy path.

---

## Deliberately out of P0

Not cut for lack of value. Cut so the P0 build lands.

| Cut | Why, and what to preserve |
|---|---|
| Error handling and recovery states | Wrong codes, failed reads, unsupported files, offline. Fail soft and silently rather than spending a screen on messages nobody reads in a demo |
| Voice input | Probably the highest-value P1 item for a Hebrew-speaking clinic. A convincing fake needs a recorder, waveform, timer and a correction pass, which is a screen's work for one optional question |
| The post-visit receipt | The reciprocity mechanism, and the reason a second form ever gets filled. Keep an `opened` field per document in the data model so it can be added without a rewrite |
| Real authentication | Faked end to end |
| Real camera access | The file picker fallback is an acceptable P0 outcome, not a degradation |
| Question branches the demo path does not use | Specified in the PRD, built only if time allows |
