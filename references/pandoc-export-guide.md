# Pandoc Export Guide

Rules and markdown structures for generating `.docx` and `.pptx` files via pandoc. Read this when you need to write the export markdown for any format.

---

## Checking for pandoc

Before any export step, run:
```bash
which pandoc
```

If pandoc is found: run the conversion automatically.
If not found: complete the markdown file, then tell the user:
> pandoc isn't installed on your system. To generate the [Word/PowerPoint] file, install it and run:
> ```
> brew install pandoc          # Mac
> winget install pandoc        # Windows
> ```
> Then: `pandoc [file.md] -o [file.docx/pptx]`

---

## Course → Word Document (`course.md` → `course.docx`)

The course docx is a **linear, readable version** of the course — no interactivity, no animations. It's a clean document someone can read offline, print, or share.

### Pandoc command
```bash
pandoc course.md -o course.docx --from markdown --to docx
```

### Markdown structure

```markdown
---
title: "[Course Title]"
subtitle: "How [App Name] Works"
---

# Module 1: [Module Title]

## [Screen/Section Title]

[2–4 sentence summary of this screen's content. Plain English. No jargon without definition.]

## Key Concepts

**[Term]**: [Plain-English definition in one sentence.]

**[Term]**: [Definition.]

## How the Code Works

Here's what happens in `[filename]`:

\`\`\`[language]
[actual code snippet from the codebase — exact copy, no modification]
\`\`\`

**In plain English:** [1–3 sentences explaining what this code does.]

> **Key insight:** [The "aha!" callout from this screen — the universal CS insight.]

## [Quiz/Exercise Title]

**Question:** [The quiz question from this module.]

**Answer:** [The correct answer with a brief explanation of why.]

---

# Module 2: [Module Title]

[...repeat structure...]
```

### Rules for course.md

- Use `---` (horizontal rule) between modules — pandoc treats this as a page break in docx.
- Use `#` for module titles, `##` for screens/sections within a module.
- Code blocks: fenced with triple backticks and language identifier.
- Key callouts: use `>` blockquote formatting. Word renders these as styled quote blocks.
- Quiz answers: always include answers in the docx (unlike the HTML course where answers are revealed on click). It's a reference document.
- Skip purely visual elements (animations, drag-and-drop) — describe them in a sentence instead: "The data flows from the browser → API server → database, returning a response at each step."
- Every code snippet must be an exact copy from the codebase.
- No HTML tags — they won't convert cleanly.

---

## Slides → PowerPoint (`slides.md` → `slides.pptx`)

Pandoc converts a specially-structured Markdown file into a real `.pptx` file using PowerPoint's built-in theme styles.

### Pandoc command
```bash
pandoc slides.md -o slides.pptx --from markdown --to pptx
```

To apply a custom reference theme (optional, advanced):
```bash
pandoc slides.md -o slides.pptx --reference-doc=reference.pptx
```

### Markdown structure

```markdown
---
title: "[Presentation Title]"
subtitle: "[One-line description of the codebase]"
author: "[Presenter name or team]"
date: "[Date]"
---

# [Section Name]

## [Slide Title — make it a statement, not a topic label]

- Fragment, not a sentence
- Lead with noun or verb
- Max 5 bullets

::: notes
What the speaker says out loud. Full sentences, 3–5 sentences total.
What to emphasize. How to transition to the next slide.
:::

## [Code Slide Title]

\`\`\`[language]
[code snippet — max 15 lines]
\`\`\`

→ [1–2 annotation lines explaining what to look at]

::: notes
Speaker notes for this code slide.
:::

## [Visual/Architecture Slide Title]

[For architecture slides, describe the diagram in text — pandoc can't render HTML diagrams in pptx.
Use a simple ASCII/text representation:]

```
Browser → API Server → Database
              ↓
          Redis Cache
```

[1–2 sentences explaining the diagram.]

::: notes
Speaker notes.
:::

# [Next Section Name]

## [Slide Title]

...

---

## Summary

### 3 Things to Remember

- **[Takeaway 1]** — one sentence
- **[Takeaway 2]** — one sentence
- **[Takeaway 3]** — one sentence

::: notes
Read each takeaway slowly. Ask if anyone wants to add to the list.
:::

## Questions?

[Contact or next steps]

::: notes
Open the floor. If no questions come immediately, have one ready: "A question I often get is..."
:::
```

### Pandoc pptx slide rules

- `# Heading` → section divider slide (full-bleed title, accent background in default theme)
- `## Heading` → content slide
- Content under `##` → slide body
- `::: notes ... :::` → speaker notes (visible in PowerPoint's presenter view)
- `---` → explicit slide break (use when you need a slide with no heading)
- **No HTML** — pandoc's pptx writer ignores HTML tags entirely
- **Architecture diagrams**: use ASCII text representations — pandoc cannot render CSS diagrams into pptx
- **Images**: if you have image files, you can include them with `![alt](path/to/image.png)` — pandoc embeds them in the pptx

### What the pptx output looks like

Pandoc generates a pptx using PowerPoint's default "blank" theme unless a reference doc is provided. The output is fully editable in PowerPoint or Google Slides. The user can:
- Apply any PowerPoint theme after opening
- Move/resize elements
- Add their company branding
- Export to PDF from within PowerPoint

Tell the user: "The `.pptx` file uses PowerPoint's default styling — you can apply your own theme in PowerPoint or Google Slides after opening it."

---

## Workshop Handout → Word Document (`workshop.md` → `workshop.docx`)

### Pandoc command
```bash
pandoc workshop.md -o workshop.docx --from markdown --to docx
```

The `workshop-handout-template.md` is already structured for clean pandoc conversion. Follow those rules:
- `---` for page breaks between segments
- No HTML tags
- Simple tables only (2–3 columns)
- Generous blank lines for answer areas

---

## Common Pandoc Failures

- **HTML tags in markdown** — pandoc silently drops them in docx/pptx output. Always use pure Markdown.
- **Complex tables** — stick to simple 2–3 column tables. Nested tables break.
- **Missing `::: notes :::` closing tag** — always close the notes div. Unclosed divs corrupt the pptx.
- **Code blocks wider than slide** — pandoc wraps code at slide edges in pptx. Keep snippets under 80 chars wide or they'll wrap awkwardly.
- **Long bullet points** — pandoc's pptx writer doesn't auto-size text. Long bullets will overflow the slide box. Keep bullets under 10 words.
- **pandoc not found** — check with `which pandoc` first. Never fail silently; always tell the user what command to run.
