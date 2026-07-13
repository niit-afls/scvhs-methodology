# AI Decision Log — Sprint 1 (Worked Example)

> This is a WORKED EXAMPLE showing you the standard of entries expected.
> Your own log will differ — your spec, your AI output, your defects.
> Use `AI_Decision_Log_Template.md` as your blank starting point.

---

**Learner Name:** Priya Sharma
**Sprint Number:** 1
**Sprint Title:** Structure a Web Page Using Semantic HTML5 Elements
**Date:** 2026-06-10
**Spec file referenced:** `Spec_S01_Portfolio_Structure.md`
**AI-generated file reviewed:** `portfolio-ai-generated.html`

---

## Entries

---

### Entry 1: Document Scaffold

**What this construct does:**
Sets up the HTML5 document. Declares DOCTYPE, opens the html element with a lang attribute, and puts metadata (charset, viewport, title) inside head.

**Does it match the spec?**
`Partial`

**Defect found:**
Spec required `<html lang="en">`. AI generated `<html>` with no lang attribute. This means the document language is undeclared — screen readers cannot determine which language to use.

**How I caught it:**
Compared line-by-line with the spec. Spec acceptance criteria explicitly listed `lang` attribute.

**Fix applied:**
Changed `<html>` to `<html lang="en">` in the AI-generated file.

---

### Entry 2: Masthead — header element

**What this construct does:**
The top section of the page. Contains the site title and a navigation bar with links to each section.

**Does it match the spec?**
`Partial`

**Defect found:**
Spec required a `nav` element inside `header` containing an unordered list of 4 links. AI generated the links as bare `<a>` elements directly inside `<header>`, with no `<nav>` wrapper and no `<ul>/<li>` structure. Navigation landmarks are invisible to screen readers without `<nav>`.

**How I caught it:**
Opened DevTools Accessibility pane. The page showed no navigation landmark in the landmark list. Compared with my hand-built version which had `<nav>`.

**Fix applied:**
Wrapped the four `<a>` elements in a `<nav><ul>` structure. Each link is now `<li><a href="...">`.

---

### Entry 3: h1 — page title

**What this construct does:**
The main heading of the page — the developer's name — used by search engines and screen readers as the primary topic of the page.

**Does it match the spec?**
`No`

**Defect found:**
Spec required exactly one `h1` on the page. AI generated two: one in the header for the developer's name, and one in the main section titled "Welcome to my portfolio." This violates the acceptance criterion and confuses both search engines and screen readers about which heading is the primary topic.

**How I caught it:**
Searched the file for `<h1` using Ctrl+F — found 2 matches. Also confirmed in DevTools Accessibility pane under Headings — both appeared at the same level.

**Fix applied:**
Changed the second `<h1>Welcome to my portfolio</h1>` to a `<p>` with a class for styling later. The welcome statement is descriptive content, not a page-level heading.

---

### Entry 4: Projects section — section vs article decision

**What this construct does:**
The section that groups all three projects together, with each project displayed as an individual entry.

**Does it match the spec?**
`No`

**Defect found:**
Spec required each project to be wrapped in an `<article>` element because each project is self-contained content that could stand alone. AI generated `<div class="project">` for each project inside a `<section>`. This is structural div soup — the div has no semantic meaning.

**How I caught it:**
Compared the AI structure with my hand-built version. In my version I had used `<article>` based on the section vs article rule from sprint: article = self-contained/syndicatable. A project entry stands alone — it has its own heading, description, and link. That is an article, not a div.

**Fix applied:**
Replaced each `<div class="project">` with `<article>`. No other change needed — the content inside was correct.

---

### Entry 5: About section

**What this construct does:**
A section introducing the developer — brief bio and background.

**Does it match the spec?**
`Yes`

**Defect found:**
None.

**How I caught it:**
Compared with spec: section element used correctly, h2 heading present, paragraph content present.

**Fix applied:**
None required.

---

### Entry 6: Contact section

**What this construct does:**
A section with contact information — email and GitHub links.

**Does it match the spec?**
`Partial`

**Defect found:**
Both links exist but the link text is not descriptive. AI generated `<a href="mailto:...">Click here</a>` and `<a href="https://github.com/...">Here</a>`. "Click here" and "Here" are meaningless to a screen reader user navigating by links. Spec said "contact information is accessible."

**How I caught it:**
Navigated the page using keyboard Tab key and read each link out loud as a screen reader would announce it. "Click here" gives no information about destination.

**Fix applied:**
Changed link text to `<a href="mailto:...">Email me at priya@email.com</a>` and `<a href="https://github.com/...">GitHub: github.com/priyasharma</a>`.

---

### Entry 7: Footer

**What this construct does:**
Bottom of the page with copyright text.

**Does it match the spec?**
`Yes`

**Defect found:**
None. `<footer>` used correctly, copyright text present.

**How I caught it:**
Compared with spec.

**Fix applied:**
None required.

---

## Summary

**Total constructs reviewed:** 7
**Total defects found:** 5
**Defects fixed:** 5

**What the AI got right:**
- About section: correct use of `<section>`, `<h2>`, and `<p>`. No changes needed.
- Footer: correct use of `<footer>` element.
- All heading levels below h1 were consistent — the AI used `<h2>` for section titles and `<h3>` for project names. Hierarchy was logical.
- DOCTYPE, meta charset, and meta viewport were all present and correct.

**Patterns in the defects:**
The AI consistently chose structural elements that look correct in the browser but carry no semantic meaning — `<div class="project">` instead of `<article>`, bare `<a>` links without `<nav>`. The AI optimised for visual output. It did not reason about accessibility or document outline. Every defect I found was a case where the AI chose a generic element over a specific semantic one.

---

## Reflection

The AI diverged most on the navigation structure (no `<nav>`) and the use of `<div>` for project entries instead of `<article>`. I knew they were wrong because my spec was explicit: "each project is a self-contained article element" and "nav element containing 4 links." When the AI output did not match those words exactly, I had a clear basis to flag it. The spec was the contract — anything that broke the contract was a defect.
