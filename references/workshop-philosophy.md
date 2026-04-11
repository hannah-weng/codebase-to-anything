# Workshop Philosophy

Rules for writing high-quality workshop materials from a codebase. Read this before writing `workshop.html` or `workshop.md`. These rules govern both the facilitator guide and the participant handout.

---

## The Two Documents

**`workshop.html` — Facilitator Guide**
For the person leading the room. Verbose and directive. Contains: exact timing, what to say, what to do, what to watch for, anticipated questions with answers, and transition cues.

**`workshop.md` → `workshop.docx` — Participant Handout**
For the people attending. Spare and spacious. Contains: concept summaries, key vocabulary, exercise worksheets with room to write, a glossary, and a notes page. No facilitator script.

These documents are complementary, not duplicates. The handout is the participant's reference *after* the session — it should make sense without the facilitator's words.

---

## Timing Architecture

Default assumption: **half-day workshop (3 hours of content, ~3.5 hours with breaks)**.

Adjust based on codebase complexity:
- Simple codebase (CLI tool, small library): 1.5–2 hours
- Mid-complexity (web app, API service): 2.5–3 hours
- Complex codebase (full-stack, microservices, monorepo): 3–4 hours

**Segment length rules:**
- Minimum: 20 minutes (shorter isn't worth a dedicated segment)
- Maximum: 45 minutes (attention collapses after this without a break)
- Mix instruction-heavy and activity-heavy segments to maintain pace

**Mandatory breaks:**
- One 10-minute break every 60–90 minutes of content
- For a 3-hour workshop: break at 60 min and 120 min
- Always show breaks in the agenda — participants need to know when relief is coming

**Time budget by segment type:**

| Segment Type | Duration |
|---|---|
| Concept introduction | 10–15 min |
| Code walkthrough / live trace | 15–20 min |
| Hands-on exercise | 20–30 min |
| Group discussion | 10–15 min |
| Q&A block | 10 min |
| Break | 10 min |

**Add 20% buffer to every estimate.** Real workshops always run long. If you estimated 15 minutes, plan for 18.

---

## Facilitator Guide Structure (workshop.html)

Each segment follows this structure, in order:

1. **Segment header**: segment number, title, duration badge
2. **Objectives**: 1–3 bullet points ("By the end of this segment, participants can…")
3. **Materials / setup**: anything the facilitator needs to prepare (browser tab open, example ready, etc.)
4. **Facilitator script**: what to say and do, in chronological order, with timing markers every 5 minutes
5. **Questions to ask the room**: 2–3 open-ended questions with follow-up probes
6. **Exercise brief** (if applicable): full instructions so the facilitator can explain it verbally
7. **Anticipated questions and answers**: 2–4 common participant questions with suggested responses
8. **Transition note**: one sentence bridging to the next segment

**HTML class conventions:**
- `.facilitator-say` — green background — what to say out loud
- `.facilitator-do` — blue background — what to do (open file, navigate to URL, etc.)
- `.watch-for` — amber background — signals that indicate participant confusion or engagement
- `.exercise-brief` — purple background — exercise instructions
- `.anticipated-qa` — neutral background — Q&A pairs
- `.transition-note` — italic, gray — bridging sentence

---

## Participant Handout Structure (workshop.md)

The Markdown file must be designed for clean pandoc conversion to Word.

**Pandoc-friendly Markdown rules:**
- `#`, `##`, `###` headings — clean Word heading styles
- `- ` bullet lists — Word list styles
- `**bold**` — Word bold
- `> ` blockquotes — Word quote style (use for key definitions)
- Fenced code blocks — monospace in Word
- `---` horizontal rules — page breaks in Word (use to separate major sections)
- Simple tables (2–3 columns max)

**Do NOT use:**
- HTML tags (don't convert cleanly)
- Complex nested tables
- Images (unless the user provides paths)
- Inline CSS or custom styles

**Handout sections (in order):**

```
# [Workshop Title]

**Date:** _______________   **Facilitator:** _______________   **Your Name:** _______________

## What This Workshop Covers
[2–3 sentence overview]

## Learning Objectives
By the end of this workshop, you will be able to:
1. [objective 1]
2. [objective 2]
3. [objective 3]

## Agenda
| Time | Segment | Duration |
|------|---------|----------|
| ...  | ...     | ...      |

---

## Segment 1: [Title]

### Key Concepts
[2–3 sentence summary]

### Vocabulary
**[term]**: [plain-English definition]
**[term]**: [plain-English definition]

### Exercise: [Exercise Name]
*[time] — [Individual / Pairs / Group]*

[Exercise prompt]

Your answer:

____________________________________________________
____________________________________________________
____________________________________________________

### Notes
____________________________________________________
____________________________________________________
____________________________________________________

---
[...repeat for each segment...]

## Glossary
**[term]**: [definition]

## After This Workshop
Things to try:
- [ ] [action item 1]
- [ ] [action item 2]

What I want to learn more about:
____________________________________________________
```

---

## Exercise Design Rules

Good exercises for technical workshops:

**Time-boxed**: Always specify exact minutes. "10 minutes individual, then 5 minutes share-out."

**Tangible output**: Participants produce something they take away — a filled diagram, a written decision, a prioritized list.

**Grounded in the actual codebase**: Exercises reference real files, real components, real scenarios. No generic hypotheticals.

**Non-coding**: Participants trace, annotate, decide, and discuss. They do not write code.

**Leveled — choose one:**
- *Individual* — everyone works alone, then share-out
- *Pairs* — work with a neighbor
- *Group* — full-room discussion, facilitator writes responses on a board

**Exercise types (pick the most appropriate):**

| Exercise Type | What participants do |
|---|---|
| Architecture mapping | Draw arrows between components on a blank diagram |
| Debugging triage | Given a bug symptom, identify likely components and why |
| Feature planning | "Which files change if we add X feature?" |
| Trade-off analysis | "Why did this codebase choose A over B?" |
| Sequence ordering | Put a data-flow sequence in the correct order |
| Vocabulary matching | Match technical terms to plain-English definitions |

---

## Design for the Facilitator HTML

The `workshop.html` is read by a facilitator on a laptop while talking. Design for this:

- **Large base font**: 18px minimum. They're glancing at this while talking, not reading.
- **Color-coded segments**: consistent colors for say/do/watch-for/exercise so the facilitator can orient instantly.
- **Visible timing**: the current running time should be prominently visible in a sidebar or badge, not buried in text.
- **Print-friendly**: include `@media print` styles. Some facilitators prefer a printed guide. In print: collapse colors to borders only, remove background fills, ensure no content is cut across page breaks.
- **Two-column layout**: narrow left column for timing/type badges; wide right column for content. On print, collapse to single column.
- **No horizontal scrolling**: all content fits the viewport width.

---

## Common Failures (Gotchas)

- **Facilitator guide that's just slide notes** — it needs a full script, not bullets. The facilitator shouldn't have to improvise from fragments.
- **Participant handout with no blank space** — people need room to write. Be generous with exercise answer areas. Triple the space you think you need.
- **Exercises that require coding** — always keep activities to tracing, annotating, and deciding. This is for non-technical participants.
- **Forgetting break time in the agenda** — always budget breaks explicitly and show them in the agenda. Participants need to know when they can breathe.
- **Timing estimates that assume everything goes smoothly** — add 20% buffer to every estimate. Real workshops run long.
- **Handout that duplicates the facilitator guide** — the handout is the participant's reference, not a transcript. Omit facilitator notes entirely.
- **Abstract exercises** — "discuss the trade-offs of this pattern" with no grounding in the actual codebase produces vague, unproductive discussion. Always anchor to specific files or components.
- **No transition notes** — abrupt segment endings disorient participants. Always include a bridging sentence before each break and each new segment.
