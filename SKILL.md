---
name: codebase-to-anything
description: "Turn any codebase into a learning artifact in the format that fits your audience. Three output formats: (1) interactive HTML course for self-paced learners, (2) reveal.js presentation slides for client or stakeholder presentations, (3) workshop materials (HTML facilitator guide + Word-ready participant handout) for live training sessions. Trigger phrases include: 'turn this into a course', 'make slides from this codebase', 'create a presentation', 'build a workshop', 'training materials for this project', 'explain this codebase interactively', 'teach this code', 'show this to a client', and similar variants."
---

# codebase-to-anything

Transform any codebase into a learning artifact — choose the format that fits your audience and context. The output is always self-contained, requires no setup, and opens directly in the browser or a standard desktop app.

## First-Run Welcome

When the skill is first triggered and the user hasn't specified a codebase or format yet, introduce yourself and explain what you do:

> **I can turn any codebase into a learning artifact — interactive course, presentation slides, or workshop materials.**
>
> First, point me at a project:
> - **A local folder** — e.g., "turn ./my-project into slides"
> - **A GitHub link** — e.g., "make a workshop from https://github.com/user/repo"
> - **The current project** — if you're already in a codebase, just say "turn this into a course"
>
> Then tell me the format you want (or I'll ask):
> - **Course** — interactive HTML for self-paced learning, with animations, quizzes, and code translations
> - **Slides** — a reveal.js presentation for stakeholder demos or client walkthroughs
> - **Workshop** — a facilitator guide (HTML) + participant handout (Word-ready) for live training sessions

If the user provides a GitHub link, clone the repo first (`git clone <url> /tmp/<repo-name>`) before starting the analysis. If they say "this codebase" or similar, use the current working directory.

---

## Format Selection

**Detect the format from the trigger phrase when possible:**

| If the user mentions… | Format |
|---|---|
| "course", "interactive", "tutorial", "learn", "teach", "self-paced" | **Course** |
| "slides", "presentation", "deck", "PowerPoint", "PPT", "show to client", "stakeholder" | **Slides** |
| "workshop", "training", "facilitator", "hands-on", "participants", "live session" | **Workshop** |

**If the trigger phrase is ambiguous, ask once:**

> I can turn this codebase into three different formats. Which would you like?
>
> 1. **Course** — Interactive single-page HTML for self-paced learning. Scroll-based modules, animations, quizzes, and code-with-plain-English translations. Best for: learners going through it on their own.
>
> 2. **Slides** — A reveal.js presentation that opens in the browser and can be exported to PDF or PowerPoint. Best for: stakeholder presentations, client demos, team onboarding.
>
> 3. **Workshop** — Two files: an HTML facilitator guide (timing, speaker notes, exercises) and a Markdown participant handout that converts to Word via pandoc. Best for: live, facilitator-led training sessions.

**Never guess and build the wrong format.** If the intent is unclear, always ask before starting Phase 1.

---

## Who This Is For

The target learner is a **"vibe coder"** — someone who builds software by instructing AI coding tools in natural language, without a traditional CS education. They may have built this project themselves (without looking at the code), or they may have found an interesting open-source project on GitHub and want to understand how it's built.

**Assume zero technical background.** Every CS concept needs to be explained in plain language. No jargon without definition. No "as you probably know." The tone should be like a smart friend explaining things, not a professor lecturing.

**Their goals are practical, not academic:**
- Have enough technical knowledge to effectively **steer AI coding tools**
- **Detect when AI is wrong** — spot hallucinations, catch bad patterns
- **Intervene when AI gets stuck** — break out of bug loops, debug issues
- Build more advanced software with **production-level quality**
- Be **technically fluent** enough to discuss decisions with engineers confidently
- **Acquire the vocabulary of software** — learn precise technical terms

**They are NOT trying to become software engineers.** They want coding as a superpower that amplifies what they're already good at.

---

## Why This Approach Works

This skill inverts traditional CS education. The old model is: memorize concepts for years → eventually build something → finally see the point (most people quit before step 3). This model is: **build something first → experience it working → now understand how it works.**

The learner already has context that traditional students don't — they've *used* the app, they know what it does, they may have even described its features in natural language. The output meets them where they are: "You know that button you click? Here's what happens under the hood when you click it."

Every format answers **"why should I care?"** before "how does it work?" The answer is always practical: *because this knowledge helps you steer AI better, debug faster, or make smarter architectural decisions.*

---

## The Process

Phase 1 (codebase analysis) is **identical for all formats**. After Phase 1, the paths diverge based on the chosen format.

---

### Phase 1: Codebase Analysis (All Formats)

Before writing any output, deeply understand the codebase. Read all the key files, trace the data flows, identify the "cast of characters" (main components/modules), and map how they communicate. Thoroughness here pays off — the more you understand, the better the output.

**What to extract:**
- The main "actors" (components, services, modules) and their responsibilities
- The primary user journey (what happens when someone uses the app end-to-end)
- Key APIs, data flows, and communication patterns
- Clever engineering patterns (caching, lazy loading, error handling, etc.)
- Real bugs or gotchas (if visible in git history or comments)
- The tech stack and why each piece was chosen

**Figure out what the app does yourself** by reading the README, the main entry points, and the UI code. Don't ask the user to explain the product — they may not be familiar with it either.

---

## FORMAT A: COURSE

An interactive single-page HTML course with scroll-based navigation, animated visualizations, embedded quizzes, and plain-English code translations. Output is a **directory** containing per-module HTML files assembled into a single `index.html`.

### Phase 2A: Course Curriculum Design

Structure the course as **4-6 modules**. Most courses need 4-6. Only go to 7-8 if the codebase genuinely has that many distinct concepts worth teaching. Fewer, better modules beat more, thinner ones.

The arc always starts from what the learner already knows (the user-facing behavior) and moves toward what they don't (the code underneath).

| Module Position | Purpose | Why it matters for a vibe coder |
|---|---|---|
| 1 | "Here's what this app does — and what happens when you use it" | Start with the product, then trace a core user action into the code. |
| 2 | Meet the actors | Know which components exist so you can tell AI "put this logic in X, not Y" |
| 3 | How the pieces talk | Understand data flow so you can debug "it's not showing up" problems |
| 4 | The outside world (APIs, databases) | Know what's external so you can evaluate costs, rate limits, and failure modes |
| 5 | The clever tricks | Learn patterns (caching, chunking, error handling) so you can request them from AI |
| 6 | When things break | Build debugging intuition so you can escape AI bug loops |
| 7 | The big picture | See the full architecture so you can make better decisions |

This is a **menu, not a checklist**. Pick the modules that serve the codebase.

**Each module should contain:**
- 3-6 screens (sub-sections that flow within the module)
- At least one code-with-English translation
- At least one interactive element (quiz, visualization, or animation)
- One or two "aha!" callout boxes with universal CS insights
- A metaphor that grounds the technical concept in everyday life — but NEVER reuse the same metaphor across modules, and NEVER default to the "restaurant" metaphor. Pick metaphors that organically fit the specific concept.

**Mandatory interactive elements (every course must include ALL of these):**
- **Group Chat Animation** — at least one across the course
- **Message Flow / Data Flow Animation** — at least one across the course
- **Code ↔ English Translation Blocks** — at least one per module
- **Quizzes** — at least one per module
- **Glossary Tooltips** — on every technical term, first use per module

**Do NOT present the curriculum for approval — just build it.**

**After designing the curriculum, decide which build path to use:**
- **Simple codebase** (single-purpose CLI, small web app, library, 5 or fewer modules) → go directly to Phase 3A Sequential.
- **Complex codebase** (full-stack app, multiple services, monorepo, 6+ modules) → go to Phase 2A.5 first, then Phase 3A Parallel.

### Phase 2A.5: Module Briefs (complex codebases only)

For complex codebases, write a brief for each module before writing any HTML. This enables parallel writing — each brief gives an agent everything it needs without re-reading the codebase.

Read `references/module-brief-template.md` for the template structure. Read `references/content-philosophy.md` for the content rules.

**For each module, write a brief to `course-name/briefs/0N-slug.md` containing:**
- Teaching arc (metaphor, opening hook, key insight)
- Pre-extracted code snippets (copy-pasted from the codebase with file paths and line numbers)
- Interactive elements checklist with enough detail to build them
- Which sections of which reference files the writing agent needs
- What the previous and next modules cover (for transitions)

### Phase 3A: Build the Course

The course output is a **directory**, not a single file. All CSS and JS are pre-built reference files — never regenerate them.

**Check for pandoc before starting:** Run `which pandoc`. Note whether it's available — you'll need it at the end for the docx export.

**Output structure:**
```
course-name/
  styles.css       ← copied verbatim from assets/styles.css
  main.js          ← copied verbatim from scripts/main.js
  _base.html       ← customized shell (title, accent color, nav dots)
  _footer.html     ← copied verbatim from assets/_footer.html
  build.sh         ← copied verbatim from scripts/build.sh
  briefs/          ← module briefs (complex codebases only, can delete after build)
  modules/
    01-intro.html
    02-actors.html
    ...
  index.html       ← assembled by build.sh (do not write manually)
  course.md        ← linear readable version (Markdown source for docx export)
  course.docx      ← Word document (only if pandoc available)
```

**Step 1 (both paths): Setup** — Create the course directory. Copy these four files verbatim using Read + Write:
- `assets/styles.css` → `course-name/styles.css`
- `scripts/main.js` → `course-name/main.js`
- `assets/_footer.html` → `course-name/_footer.html`
- `scripts/build.sh` → `course-name/build.sh`

**Step 2 (both paths): Customize `_base.html`** — Read `assets/_base.html`, then write it to `course-name/_base.html` with exactly three substitutions:
- Both instances of `COURSE_TITLE` → the actual course title
- The four `ACCENT_*` placeholders → the chosen accent color values
- `NAV_DOTS` → one `<button class="nav-dot" ...>` per module

**Step 3: Write modules** — This is where the paths diverge.

#### Sequential path (simple codebases)

Read `references/content-philosophy.md` and `references/gotchas.md`. Then write modules one at a time. For each module, write `course-name/modules/0N-slug.html` containing only the `<section class="module" id="module-N">` block and its contents. Do not include `<html>`, `<head>`, `<body>`, `<style>`, or `<script>` tags.

Read `references/interactive-elements.md` for HTML patterns. Read `references/design-system.md` for visual conventions.

#### Parallel path (complex codebases)

Dispatch modules to subagents in batches of up to 3. Each agent receives:
- Its module brief (from `course-name/briefs/`)
- `references/content-philosophy.md` and `references/gotchas.md`
- Only the sections of `references/interactive-elements.md` and `references/design-system.md` listed in the brief

Each agent writes its module file(s) to `course-name/modules/`. After all agents finish, do a quick consistency check: nav dots match modules, transitions are coherent, no obvious tone shifts.

**Step 4 (both paths): Assemble** — Run `build.sh` from the course directory:
```bash
cd course-name && bash build.sh
```
This produces `index.html`. Open it in the browser.

**Step 5 (both paths): Generate Word export** — Read the "Course → Word Document" section of `references/pandoc-export-guide.md`. Write `course-name/course.md` — a linear, readable version of the course content structured for pandoc. Rules:
- `#` for module titles, `##` for screens/sections within each module
- `---` between modules (pandoc treats this as a page break in docx)
- Code blocks with fenced triple-backtick syntax
- Key callouts as `>` blockquotes
- Quiz answers included (unlike the interactive HTML, the docx is a reference document)
- For animation/interactive elements: describe them in a sentence ("The data flows from browser → API → database")
- No HTML tags

Then convert to Word:
```bash
cd course-name && pandoc course.md -o course.docx --from markdown --to docx
```

If pandoc is not available, tell the user:
> pandoc isn't installed. To generate the Word document, install it and run:
> `brew install pandoc` (Mac) or `winget install pandoc` (Windows)
> Then: `cd course-name && pandoc course.md -o course.docx`

**Critical rules:**
- **Never regenerate** `styles.css` or `main.js` — always copy from references
- Module files contain only `<section>` content — no boilerplate
- Use CSS `scroll-snap-type: y proximity` (NOT `mandatory`)
- Use `min-height: 100dvh` with `100vh` fallback on `.module`
- Interactive element JS is in `main.js`; wire up via `data-*` attributes and CSS class names as shown in `references/interactive-elements.md`

### Phase 4A: Review and Open (Course)

After running `build.sh`, open `index.html` in the browser. Walk the user through what was built and ask for feedback on content, design, and interactivity.

---

## FORMAT B: SLIDES

A reveal.js presentation that opens in the browser. Output is a **directory** with one file.

### Phase 2B: Slides Outline

After Phase 1 analysis, design the slide deck structure.

**Slide count targets:**
- 10-minute overview: 8–12 slides
- 30-minute session: 14–20 slides
- 45-minute deep-dive: 18–25 slides
- Never exceed 25. If you're over, cut — don't compress.

**Standard deck structure:**
1. Title slide
2. Agenda slide (list of sections)
3. Section divider → content slides → repeat for each section
4. Summary slide ("3 Key Takeaways")
5. Q&A / Closing slide

**Do NOT present the outline for approval — just build it.**

Read `references/slides-philosophy.md` before writing any slide HTML. It contains the full rules for bullet writing, speaker notes, architecture diagrams, animations, and gotchas.

### Phase 3B: Build Slides

**Output structure:**
```
project-slides/
  slides.html    ← reveal.js presentation (browser, fullscreen, speaker notes)
```

**Step 1:** Read `references/slides-philosophy.md` and `assets/slides-template.html`.

**Step 2:** Create `project-slides/` directory.

**Step 3:** Write `project-slides/slides.html`. Use `assets/slides-template.html` as the shell — do NOT copy it verbatim. Customize it:
- Replace `PRESENTATION_TITLE` with the actual title
- Replace `PRESENTATION_SUBTITLE` with a one-line description of the codebase
- Replace `PRESENTER_NAME` and `PRESENTATION_DATE`
- Replace `ACCENT_HEX`, `ACCENT_DARK`, `ACCENT_LIGHT` with a chosen color (see palette options in `assets/slides-template.html`)
- Replace the placeholder `<section>` elements with actual content slides
- Replace the agenda list items with the real sections

**Step 4:** Open `slides.html` in the browser. Tell the user these controls:
- `Space` / `→` — advance slide
- `S` — speaker notes view (open in separate window for presenting)
- `F` — fullscreen
- `O` — overview of all slides

**Critical rules for slides.html:**
- reveal.js via CDN only — never copy the library locally
- Every `<section>` = one slide
- Speaker notes in `<aside class="notes">` inside every section — no exceptions
- Max 5 bullets per slide — if you need more, split the slide
- No full paragraphs — fragments only
- Code blocks: `<pre><code class="hljs language-X">` with `font-size: 0.5em` on `<pre>` if needed
- Transition: `fade` only — never `slide`, `convex`, or `zoom`

### Phase 4B: Review and Open (Slides)

Open `slides.html` in the browser and walk the user through the deck. Ask: is the scope right? Any sections to add, cut, or reorder? Any slides that need a visual instead of bullets?

---

## FORMAT C: WORKSHOP

Two files: an HTML facilitator guide and a Markdown participant handout (convertible to Word). Output is a **directory** with both files.

### Phase 2C: Workshop Structure

After Phase 1 analysis, design the workshop structure.

**Duration planning:**
- Simple codebase (CLI, library): 1.5–2 hours of content
- Mid-complexity (web app, API): 2.5–3 hours
- Complex (full-stack, microservices): 3–4 hours

**Segment architecture:**
- Segments: 20–45 minutes each
- Mix instruction-heavy and activity-heavy segments
- Break every 60–90 minutes (10 minutes each)
- Add 20% buffer to every estimate — workshops always run long

**Standard workshop arc:**
1. Welcome + orientation (15 min) — what the app does, what we'll cover, why it matters
2. Architecture overview (20–30 min) — the "cast of characters" and how they fit together
3. Core flow walkthrough (20–30 min) — trace a user action through the code
4. [Format-specific section based on codebase] (20–45 min)
5. Hands-on exercise (20–30 min) — participants apply what they learned
6. Debugging and common problems (20–30 min) — how to recognize and fix issues
7. Q&A and wrap-up (15 min)

Adapt this arc to the codebase. Not every codebase needs all 7 segments.

**Check for pandoc before starting:** Run `which pandoc`. Note whether it's available. If not, warn the user at the end and provide the install command (`brew install pandoc` on Mac, `winget install pandoc` on Windows).

**Do NOT present the structure for approval — just build it.**

Read `references/workshop-philosophy.md` before writing any workshop files.

### Phase 3C: Build Workshop

**Output structure:**
```
project-workshop/
  workshop.html    ← facilitator guide (open in browser)
  workshop.md      ← participant handout (Markdown)
  workshop.docx    ← Word file (only if pandoc available)
```

**Step 1:** Read `references/workshop-philosophy.md`, `assets/workshop-facilitator-template.html`, and `references/workshop-handout-template.md`.

**Step 2:** Create `project-workshop/` directory.

**Step 3: Write `workshop.html`** — the facilitator guide. Use `assets/workshop-facilitator-template.html` as the shell. Customize it:
- Replace `WORKSHOP_TITLE`, `WORKSHOP_DATE`, `WORKSHOP_DURATION`, `WORKSHOP_AUDIENCE`
- Fill in the agenda table with real segments and timing
- Write one `.segment` block per segment, following the template pattern
- Each segment must include: objectives, setup notes, facilitator script with timing markers, room questions, watch-fors, exercise brief (if applicable), anticipated Q&A, and a transition note
- The facilitator script must be full sentences — not bullets. The facilitator should be able to read it aloud.

**Step 4: Write `workshop.md`** — the participant handout. Use `references/workshop-handout-template.md` as the structure. Rules:
- Delete the HTML comment instructions at the top before saving
- No HTML tags — pandoc handles markdown only
- Use `---` for page breaks between major sections
- Exercise answer areas: generous blank lines (at least 4 per exercise)
- Keep it spare — participants write in it; blank space is the point

**Step 5:** If pandoc is available, run:
```bash
cd project-workshop && pandoc workshop.md -o workshop.docx --from markdown --to docx
```
Tell the user they can open `workshop.docx` in Microsoft Word or Google Docs. If pandoc is not available:
> I couldn't find pandoc on your system. To get the Word file, install pandoc (`brew install pandoc`) and then run: `pandoc workshop.md -o workshop.docx`

**Critical rules:**
- Facilitator guide (`workshop.html`) is for the facilitator — verbose, directive, full sentences
- Participant handout (`workshop.md`) is for attendees — sparse, spacious, no facilitator notes
- Exercises must be non-coding: participants trace, annotate, decide, discuss — never write code
- Every exercise specifies duration and level (Individual / Pairs / Group)
- Always include at least one hands-on exercise per segment over 25 minutes

### Phase 4C: Review and Open (Workshop)

Open `workshop.html` in the browser and walk the facilitator through each segment. Ask: is the timing realistic? Are the exercises grounded in real parts of the codebase? Is anything missing?

Also confirm that `workshop.md` converted cleanly if pandoc was available.

---

## Design Identity

### Course design
Read `references/design-system.md` for the full token system. Key principles:
- **Warm palette**: Off-white backgrounds, warm grays, NO cold whites or blues
- **Bold accent**: One confident accent color (vermillion, coral, teal — NOT purple gradients)
- **Distinctive typography**: Bricolage Grotesque for headings. NEVER Inter, Roboto, Arial. DM Sans for body. JetBrains Mono for code.
- **Generous whitespace**: Max 3-4 short paragraphs per screen
- **Alternating backgrounds**: Even/odd modules alternate between two warm tones
- **Dark code blocks**: IDE-style with Catppuccin-inspired syntax highlighting on deep indigo-charcoal (#1E1E2E)

### Slides design
The warm palette and typography from the course carry over. The `slides-template.html` includes theme overrides that apply the design system to reveal.js. Choose an accent color that fits the project's personality.

### Workshop design
The facilitator guide uses the same warm typography but a professional two-column layout optimized for reading on a laptop while speaking. Color-coded blocks (green = say, blue = do, amber = watch for, purple = exercise) let the facilitator orient instantly.

---

## Reference Files

Read reference files **only when you reach the relevant phase** — not upfront. This keeps context lean.

### Course format references
- **`references/content-philosophy.md`** — Visual density rules, metaphor guidelines, quiz design, tooltip rules. Read during Phase 2A and 3A.
- **`references/gotchas.md`** — Common failure checklist. Read during Phase 3A and 4A.
- **`references/module-brief-template.md`** — Template for Phase 2A.5 module briefs. Read only for complex codebases.
- **`references/design-system.md`** — Complete CSS custom properties, color palette, typography. Read during Phase 3A.
- **`references/interactive-elements.md`** — Implementation patterns for every interactive element. Read relevant sections during Phase 3A.
- **`assets/_base.html`** — HTML shell template. Read and customize during Phase 3A Step 2.
- **`assets/_footer.html`** — Footer. Copy verbatim.
- **`assets/styles.css`** — Complete CSS. Copy verbatim.
- **`scripts/main.js`** — Interactive engine. Copy verbatim.
- **`scripts/build.sh`** — Assembly script. Copy verbatim.
- **`references/pandoc-export-guide.md`** — Markdown structure and pandoc command for `.docx` export. Read the "Course → Word Document" section during Phase 3A Step 5.

### Slides format references
- **`references/slides-philosophy.md`** — Slide count rules, bullet writing, speaker notes, diagram patterns, gotchas. Read during Phase 2B and 3B.
- **`assets/slides-template.html`** — reveal.js shell with warm theme overrides. Read and customize during Phase 3B Step 3.

### Workshop format references
- **`references/workshop-philosophy.md`** — Timing architecture, facilitator guide structure, handout rules, exercise design. Read during Phase 2C and 3C.
- **`assets/workshop-facilitator-template.html`** — Facilitator guide HTML shell with color-coded block system. Read and customize during Phase 3C.
- **`references/workshop-handout-template.md`** — Participant handout Markdown structure. Read and customize during Phase 3C.
- **`references/pandoc-export-guide.md`** — Pandoc command and rules for `.docx` export. Read the "Workshop Handout" section during Phase 3C Step 5.
