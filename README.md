# Codebase to ANYTHING

A Claude Code skill that turns any codebase into a learning artifact — in the format that fits your audience.

Point it at a repo and choose how you want to explain it:

## Three Output Formats

| Format | Best for | Output |
|--------|---------|--------|
| **Course** | Self-paced learners | Interactive HTML (`index.html`) + Word document (`course.docx`) |
| **Slides** | Stakeholder presentations, client demos | Browser presentation (`slides.html`) |
| **Workshop** | Facilitator-led training sessions | Facilitator guide (`workshop.html`) + participant handout (`workshop.docx`) |

---

## Who is this for?

**Learners** — vibe coders, new team members, or anyone who built or inherited a codebase and wants to understand what's actually happening under the hood. The Course format turns any repo into a self-paced interactive experience that teaches without lecturing.

**Presenters** — developers, technical leads, or consultants who need to walk clients or stakeholders through how a system works — without losing them in code. The Slides format gives you a polished deck you can actually present.

**Trainers and facilitators** — people running onboarding sessions, internal workshops, or technical training for non-engineering teams. The Workshop format gives you a facilitator guide with timing and speaker notes, plus a participant handout they can take home.

---

## What each format looks like

### Course
Two files — an interactive HTML course and a Word document:

**Interactive HTML (`index.html`):**
No dependencies, no setup, works offline. It includes:

- **Scroll-based modules** with progress tracking and keyboard navigation
- **Code ↔ Plain English translations** — real code on the left, what it means on the right
<img width="1600" height="1190" alt="Code translation block" src="https://github.com/user-attachments/assets/40930e4a-85c2-4194-b463-6f5dd31f543a" />

- **Animated visualizations** — data flow animations, group chat between components, architecture diagrams
<img width="1600" height="642" alt="Animated data flow" src="https://github.com/user-attachments/assets/16bc2958-5c38-4e47-8414-5685d7225232" />

- **Interactive quizzes** that test *application* not memorization ("You want to add favorites — which files change?")
<img width="1600" height="978" alt="Interactive quiz" src="https://github.com/user-attachments/assets/0c5bb168-595c-4d8f-afaf-4fcb671a8f8a" />

- **Glossary tooltips** — hover any technical term for a plain-English definition
<img width="2560" height="1480" alt="Glossary tooltip" src="https://github.com/user-attachments/assets/649ee5be-9116-48b4-9d29-badbb36057d9" />


- **Fresh, distinctive design** — not the typical purple-gradient AI look

**Word document (`course.docx`, generated via pandoc):**
- Linear, readable version of the course content — all modules, code explanations, and quiz answers
- Printable, shareable, no browser required
- Requires pandoc: `brew install pandoc` (Mac) / `winget install pandoc` (Windows)

### Slides

**Browser presentation (`slides.html`):**
- Warm design with the same typography as the course
- Speaker notes mode (`S` key), fullscreen (`F`), slide overview (`O`)
- Runs offline, no setup needed

<img width="2560" height="1440" alt="Slides title slide" src="https://github.com/user-attachments/assets/3421d038-994d-4400-ae58-741473b04cd1" />
<img width="2560" height="1440" alt="Slides content slide" src="https://github.com/user-attachments/assets/427b691e-2c2c-4c72-b166-2929ae32ab1c" />


### Workshop
Two complementary documents:

**Facilitator guide (`workshop.html`):**
- Color-coded blocks: what to say (green), what to do (blue), what to watch for (amber), exercises (purple)
- Timing markers every 5 minutes through each segment
- Anticipated Q&A with suggested answers
- Print-friendly layout

<img width="2560" height="1800" alt="Workshop facilitator guide overview" src="https://github.com/user-attachments/assets/a08c080b-3f53-451f-9daf-43f83d54d879" />

<img width="2560" height="1800" alt="Workshop color-coded facilitator blocks" src="https://github.com/user-attachments/assets/757ed612-d1d1-4ddd-8065-c91eabd5efe7" />

**Participant handout (`workshop.docx`):**
- Concept summaries and key vocabulary per segment
- Exercise worksheets with space to write
- Glossary of all technical terms
- Post-workshop action items page
- Generated from Markdown via pandoc (install: `brew install pandoc`)

---

## How to use

### As a Claude Code skill

1. Copy the `codebase-to-anything` folder into `~/.claude/skills/`
2. Open any project in Claude Code
3. Say what you want to make

### Trigger phrases

**Course:**
- "Turn this into an interactive course"
- "Explain this codebase interactively"
- "Teach me how this code works"

**Slides:**
- "Make slides from this codebase"
- "Create a presentation I can show to a client"
- "Turn this into a deck for stakeholders"

**Workshop:**
- "Build a workshop from this codebase"
- "Create training materials for this project"
- "Make a facilitator guide for this repo"

**Ambiguous (will ask you to choose):**
- "Turn this codebase into something I can share"
- "Explain this to my team"

---

## Design philosophy

### Build first, understand later

This inverts traditional CS education. The old way: memorize concepts for years → eventually build something → finally see the point (most people quit before step 3). This way: **build something → experience it working → now understand how it works.**

### Show, don't tell

Every output prioritizes visuals over prose. Diagrams, animations, and structured layouts communicate faster than paragraphs.

### Quizzes and exercises test doing, not knowing

No "What does API stand for?" Instead: "A user reports stale data after switching pages. Where would you look first?" Tests whether you can *use* what you learned to solve a new problem.

### No recycled metaphors

Each concept gets a metaphor that fits *that specific idea*. Never the same metaphor twice.

### Original code only

Code snippets are exact copies from the real codebase — never modified or simplified.

---

## Skill structure

```
codebase-to-anything/
├── SKILL.md                               # Main skill instructions
├── assets/                               # HTML and CSS files (copied verbatim into output)
│   ├── _base.html                         # Course HTML shell template
│   ├── _footer.html                       # Course footer
│   ├── styles.css                         # Course design system CSS
│   ├── slides-template.html               # reveal.js shell with warm theme
│   └── workshop-facilitator-template.html # Facilitator guide HTML shell
├── references/                           # Markdown docs Claude reads during build
│   ├── content-philosophy.md              # Teaching and content rules (course)
│   ├── design-system.md                   # CSS tokens, typography, colors (course)
│   ├── interactive-elements.md            # Quiz, animation, visualization patterns (course)
│   ├── gotchas.md                         # Common failure checklist (course)
│   ├── module-brief-template.md           # Planning template for complex codebases
│   ├── slides-philosophy.md               # Slide count, bullets, notes, gotchas
│   ├── workshop-philosophy.md             # Timing, exercise design, content rules
│   ├── workshop-handout-template.md       # Participant handout Markdown template
│   └── pandoc-export-guide.md             # Markdown structures + pandoc commands for .docx/.pptx
└── scripts/                              # JS and shell scripts
    ├── main.js                            # Course interactive engine (copied verbatim)
    └── build.sh                           # Course assembly script (copied verbatim)
```

---

Built by [Hannah](https://x.com/ywhx_hannah) with Claude Code.
