# Slides Philosophy

Rules for writing high-quality presentation slides from a codebase. Read this before writing any `slides.html` content.

---

## Slide Count and Scope

- Target **12–20 slides** for a typical codebase. A 10-minute overview: 8–12 slides. A 45-minute deep-dive: 18–25.
- If you're over 25 slides, you have an essay problem, not a presentation problem. Cut, don't compress.
- Every slide should stand alone as a leave-behind — someone who missed the talk should grasp the key point just from the slide.

---

## The One-Idea Rule

**One idea per slide.** Not one section. Not one topic. One *idea*.

- If the slide title contains "and" — it's two slides.
- If the speaker notes contain more than 3 talking points — it's two slides.
- If a bullet requires a subordinate clause to make sense — split it.

---

## Slide Types

Choose from this taxonomy. Every slide should be one of these types:

| Type | Purpose | When to use |
|------|---------|-------------|
| **Title** | Presentation title, subtitle, presenter | First slide only |
| **Agenda** | Numbered list of sections | Second slide only |
| **Section divider** | Large text, accent background, section name | Between major sections |
| **Point slide** | Heading + 3–5 bullet fragments | Core content workhorse |
| **Visual slide** | Heading + one diagram or table, no bullets | Showing structure/relationships |
| **Code slide** | Heading + one code block (max 15 lines) + 1–2 annotation lines | Showing how something works |
| **Quote slide** | Large pull quote + attribution | Key insight or surprising fact |
| **Architecture slide** | Heading + system diagram (HTML/CSS boxes and arrows) | Showing system components |
| **Fragment slide** | Step-by-step reveal using `data-fragment-index` | Walking through a process |
| **Summary slide** | "3 Key Takeaways" + three bullets | Second-to-last slide only |
| **Q&A slide** | Closing — "Questions?" + contact/next steps | Last slide only |

---

## Bullet Writing Rules

Fragments, not sentences.

**Wrong:** "The system uses Redis for caching which reduces database load by preventing repeated queries."
**Right:** "Redis cache → 10× fewer DB queries"

Rules:
- Max **5 bullets** per slide. If you need 6, you need two slides.
- Lead with the noun or verb — never start with "The", "A", or "This".
- Each bullet should be self-contained: a reader skimming the deck understands it without the speaker.
- Use `→` arrows for cause-effect. Use `:` for definitions. Use `vs.` for comparisons.

---

## Speaker Notes

Every slide **must** have speaker notes in `<aside class="notes">`.

Rules:
- Write in full sentences — this is what the speaker says out loud.
- 3–5 sentences per slide: opening line, key explanation, optional example, transition to next slide.
- Never duplicate the slide text verbatim. Notes add context; they don't read the bullets back.
- The first sentence of notes should be something the speaker says before pointing at the slide content.

Example:
```html
<aside class="notes">
  Ask the audience if they've ever hit a "slow page load" issue in their app.
  That's often a symptom of what we're about to see — every user action triggering
  a fresh database hit when a cached result would do. The architecture we're looking
  at today solves this with a Redis layer between the API and the database.
  Next we'll see exactly how that layer is wired up.
</aside>
```

---

## Architecture Diagrams

Build diagrams with HTML/CSS inside `<section>` elements. No images required.

Rules:
- Use `<div>` boxes with flexbox layout — not tables.
- Max **6 boxes** per diagram. If more nodes are needed, use two slides (overview → detail).
- Use the warm color palette from the course design system:
  - Actor 1: `#D94F30` (vermillion)
  - Actor 2: `#2D8A6E` (teal)
  - Actor 3: `#7B5EA7` (plum)
  - Actor 4: `#B87333` (copper)
  - Actor 5: `#1A6B9A` (steel blue)
- Arrows: use `→` (Unicode U+2192) in text, or CSS `border-right` + `border-bottom` rotated 45°.
- Keep diagram CSS inline in a `<style>` block inside the `<section>`.

Example pattern:
```html
<section>
  <h2>How a Request Flows</h2>
  <style>
    .arch { display: flex; align-items: center; gap: 1rem; justify-content: center; font-size: 0.7em; }
    .box { padding: 0.6em 1em; border-radius: 8px; color: white; font-weight: 600; }
  </style>
  <div class="arch">
    <div class="box" style="background:#1A6B9A">Browser</div>
    <span>→</span>
    <div class="box" style="background:#D94F30">API Server</div>
    <span>→</span>
    <div class="box" style="background:#2D8A6E">Database</div>
  </div>
  <aside class="notes">Walk through the request path left to right...</aside>
</section>
```

---

## Code Slides

Rules:
- Max **15 lines** of code per slide. If the snippet is longer, extract the essential lines and add a comment like `// ... rest omitted`.
- Use `<pre><code class="hljs language-javascript">` (or the appropriate language).
- Add 1–2 annotation lines below the code block explaining what to look at.
- Reduce font size on the code block if needed: `style="font-size: 0.5em;"` on the `<pre>` tag.
- Only show code from the real codebase — never simplified or invented.

---

## Fragment Animations

Use `data-fragment-index` for step-by-step reveals on process slides.

- Only use `class="fragment"` with `fade-in` (the default). Never use `zoom`, `spin`, or `grow`.
- Assign `data-fragment-index` starting at 1 and incrementing by 1.
- Limit to **5 fragments** per slide. More is disorienting.

Example:
```html
<section>
  <h2>What Happens When You Click "Submit"</h2>
  <ol>
    <li class="fragment" data-fragment-index="1">Form data validated in the browser</li>
    <li class="fragment" data-fragment-index="2">POST request sent to <code>/api/submit</code></li>
    <li class="fragment" data-fragment-index="3">Server writes to database</li>
    <li class="fragment" data-fragment-index="4">Response returned → UI updates</li>
  </ol>
</section>
```

---

## reveal.js Configuration

Use this exact CDN version and config block. Do not deviate.

**In `<head>`:**
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/reveal.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/theme/white.css" id="theme">
```

**Before `</body>`:**
```html
<script src="https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/dist/reveal.js"></script>
<script>
  Reveal.initialize({
    hash: true,
    slideNumber: 'c/t',
    transition: 'fade',
    backgroundTransition: 'fade',
    controls: true,
    progress: true,
    center: true
  });
</script>
```

**Keyboard shortcuts to tell the user:**
- `Space` or `→` — advance
- `S` — speaker notes view
- `F` — fullscreen
- `O` — slide overview
- `Cmd+P` / `Ctrl+P` → Save as PDF (enable "Background graphics")

---

## Content Must Fit the Window

Every slide must be fully visible without scrolling. reveal.js scales the slide canvas (1280×720) to fit the viewport — but it never shrinks content that overflows *within* that canvas.

**Rules:**
- Never put more content on a slide than can comfortably fit in a 1280×720 rectangle at readable font sizes.
- If content feels tight, **split the slide** — never shrink fonts below `0.7em` for body text or `0.45em` for code.
- Lists: max 5 items. Cards: max 4 in a 2×2 grid. Code: max 15 lines.
- Always use `width: 1280, height: 720, margin: 0.08` in `Reveal.initialize()` — this locks the canvas size so the browser can scale it correctly.
- The `slides-template.html` already includes `overflow: hidden` on all sections — rely on this as a safety net, not as the primary strategy.

---

## Common Failures (Gotchas)

- **Content overflowing the slide** — split it into two slides. Never let the audience see clipped content.
- **Paragraph-length bullets** — always fragments. If you wrote a sentence, it's a bullet that needs cutting.
- **Missing speaker notes** — every slide needs notes. No exceptions.
- **Code block overflow** — if code overflows the slide, set `font-size: 0.45em` on `<pre>`.
- **Too many fragments** — more than 5 reveals per slide breaks the pacing. Split the slide.
- **No section dividers** — without them the deck feels like a wall of identical slides. Every major section needs a divider slide.
- **Wrong transition** — only `fade`. Never `slide`, `convex`, or `zoom` — they look amateurish.
- **Overloaded architecture diagrams** — max 6 boxes. If the system has 12 components, show the 4 most important for this audience.
- **Forgetting `hash: true`** — without it, you can't link directly to a slide for sharing.
