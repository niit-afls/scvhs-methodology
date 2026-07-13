# Spec_S01_Portfolio_Structure.md

**Author:** [Your name]
**Sprint:** 1 — Structure a Web Page Using Semantic HTML5 Elements
**Date:** [Date]
**SCVHS Mode:** Hand-First + Validate AI — you hand-build the portfolio HTML first, then give this spec to an AI tool, validate the AI output against your spec, and discard it. Your hand-built version ships.
**Base:** None — start from scratch

---

## Purpose

A single-page developer portfolio that communicates structure clearly to accessibility tools, search engines, and teammates — using semantic HTML5 only. No styling. No JavaScript.

---

## Structure

### 1. Document Scaffold
- `<!DOCTYPE html>`
- `<html lang="en">`
- `<head>` containing:
  - `<meta charset="UTF-8">`
  - `<meta name="viewport" content="width=device-width, initial-scale=1.0">`
  - `<title>` — developer name
- `<body>`

### 2. Masthead (`<header>` element)
- `<h1>` — developer name (exactly one on the entire page)
- `<nav>` — unordered list of 4 links: About, Projects, Contact, GitHub

### 3. Main Content (`<main>` element)

#### About section (`<section>` element)
- `<h2>` — "About Me"
- `<p>` — 2 to 3 sentences

#### Projects section (`<section>` element)
- `<h2>` — "Projects"
- Exactly 3 project entries, each as an `<article>` element:
  - `<h3>` — project name
  - `<p>` — short description
  - `<a href="#">` — link to project

#### Contact section (`<section>` element)
- `<h2>` — "Contact"
- `<p>` containing:
  - `<a href="mailto:...">` — email address written out as link text
  - `<a href="https://github.com/...">` — GitHub profile URL written out as link text

### 4. Footer (`<footer>` element)
- `<p>` — copyright text

---

## Acceptance Criteria
*(This list is your VALIDATE checklist — check every item before submitting)*

- Passes W3C Validator with zero errors
- Exactly one `<h1>` on the page
- Heading order: `h1` → `h2` (section titles) → `h3` (project names) — no levels skipped
- No `<div>` or `<span>` used structurally
- Every `<img>` has meaningful `alt` text
- `<html>` element has `lang` attribute
- Document has `<meta charset>` and `<meta name="viewport">`
- `<nav>` element present and contains only `<a>` elements with descriptive link text (not "click here")
- Each project is wrapped in `<article>` (not `<div>` or `<section>`)
- All link text is descriptive — link destination is clear without surrounding context

---

## Files to Commit

```
portfolio.html                  — your hand-built version
portfolio-ai-generated.html     — AI-generated version from this spec
AI_Decision_Log_S01.md          — your completed Decision Log
```
