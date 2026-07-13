# Spec_S02_Portfolio_Stylesheet.md

**Author:** [Your name]
**Sprint:** 2 — Style a Web Page Using CSS Properties and the Box Model
**Date:** [Date]
**SCVHS Mode:** Hand-First + Validate AI — you hand-write the full stylesheet first, then give this spec to an AI tool, validate the AI stylesheet against your spec (focus: specificity conflicts, !important, contrast), and discard it. Your hand-written stylesheet ships.
**Base:** `portfolio.html` from Sprint 1 — HTML structure does not change this sprint

---

## Purpose

Add an external CSS stylesheet to the Sprint 1 portfolio. Style all sections using the box model, a consistent spacing scale, a type scale, a colour palette with verified contrast, and one Flexbox layout.

---

## Stylesheet

**File:** `styles.css`
**Linked via:** `<link rel="stylesheet" href="styles.css">` inside `<head>` of `portfolio.html`

---

## Spacing Scale
*(All margin, padding, and gap values must come from this scale — no other numbers)*

| Name | Value |
|------|-------|
| xs   | 8px   |
| sm   | 16px  |
| md   | 24px  |
| lg   | 40px  |
| xl   | 64px  |

---

## Type Scale
*(All font-size values must use rem — base is 16px body)*

| Element | Size     | Weight |
|---------|----------|--------|
| h1      | 2.5rem   | 700    |
| h2      | 1.75rem  | 600    |
| h3      | 1.25rem  | 600    |
| p       | 1rem     | 400    |
| footer  | 0.875rem | 400    |

Body `line-height`: 1.6

---

## Colour Palette
*(Verify each contrast ratio in DevTools Accessibility panel before submitting)*

| Role        | Hex       | Used on                        | Contrast on white | AA pass |
|-------------|-----------|--------------------------------|-------------------|---------|
| Background  | `#FFFFFF` | Page background                | —                 | —       |
| Surface     | `#F5F5F5` | Project card backgrounds       | —                 | —       |
| Primary     | `#2563EB` | Links, accents                 | 5.9:1             | Yes     |
| Text        | `#1A1A1A` | Body copy                      | 16.1:1            | Yes     |
| Muted       | `#6B7280` | Tagline, footer text           | 4.6:1             | Yes     |

---

## Rules by Element

### Global reset (selector: `*, *::before, *::after`)
- `box-sizing: border-box`
- `margin: 0`
- `padding: 0`

### Body (selector: `body`)
- `font-family: Arial, sans-serif`
- `font-size: 1rem`
- `line-height: 1.6`
- `color: #1A1A1A`
- `background-color: #FFFFFF`

### Header (selector: `header`)
- `background-color: #1A1A1A`
- `padding: 16px 40px`
- `h1` inside header: `color: #FFFFFF`, `font-size: 2.5rem`
- `p` inside header (tagline): `color: #6B7280`, `font-size: 1rem`

### Navigation (selector: `nav`)
- Flexbox container: `display: flex`, `gap: 16px`, `list-style: none`
- `nav a`: `color: #FFFFFF`, `text-decoration: none`, `font-weight: 500`
- `nav a:hover` (pseudo-class): `text-decoration: underline`

### Main (selector: `main`)
- `max-width: 960px`
- `margin: 0 auto`
- `padding: 40px 16px`

### Section headings (selector: `section h2`)
- `font-size: 1.75rem`
- `margin-bottom: 24px`

### Projects grid (selector: `.projects-grid`)
- Flexbox container: `display: flex`, `flex-wrap: wrap`, `gap: 24px`

### Project card (selector: `.project-card`)
- `background-color: #F5F5F5`
- `padding: 24px`
- `h3` inside card: `font-size: 1.25rem`, `margin-bottom: 8px`
- `a` inside card: `color: #2563EB`

### Contact section (selector: `section a`)
- `color: #2563EB`

### Footer (selector: `footer`)
- `background-color: #F5F5F5`
- `padding: 24px 40px`
- `text-align: center`
- `color: #6B7280`
- `font-size: 0.875rem`

---

## Specificity Predictions
*(Write your prediction as a comment in the stylesheet BEFORE opening DevTools to verify)*

| Rule pair                         | Which wins?          | Why (specificity score)        |
|-----------------------------------|----------------------|-------------------------------|
| `nav a` vs `a`                    | `nav a`              | (0,0,2) beats (0,0,1)         |
| `.project-card h3` vs `h3`        | `.project-card h3`   | (0,1,1) beats (0,0,1)         |
| `section h2` vs `h2`             | `section h2`         | (0,0,2) beats (0,0,1)         |

---

## Acceptance Criteria
*(This list is your VALIDATE checklist — check every item before submitting)*

**Stylesheet structure**
- External stylesheet linked via `<link rel="stylesheet">` — no `<style>` blocks, no inline `style=` attributes

**Box model**
- `box-sizing: border-box` applied globally via `*` selector
- No magic numbers — every spacing value comes from the spacing scale above

**Units**
- All `font-size` values in `rem`
- Border widths in `px` only
- Margins and padding from the spacing scale

**Typography**
- `h1`, `h2`, `h3` sizes match the type scale
- Body `line-height: 1.6`

**Colour and contrast** *(verify in DevTools Accessibility panel)*
- Body text `#1A1A1A` on `#FFFFFF`: contrast ratio ≥ 4.5:1
- Link colour `#2563EB` on `#FFFFFF`: contrast ratio ≥ 4.5:1
- Muted text `#6B7280` on `#FFFFFF`: contrast ratio ≥ 4.5:1

**Flexbox**
- `nav` is a flex container — verify `display: flex` in DevTools Styles panel
- `.projects-grid` is a flex container with `flex-wrap: wrap` — verify in DevTools

**Specificity**
- Three specificity predictions written as comments in stylesheet before DevTools verification
- All three predictions correct when verified

**Hygiene**
- No `!important` anywhere in the stylesheet
- No ID selectors used for styling

---

## Files to Commit

```
portfolio.html                  — unchanged from Sprint 1 (add class attributes only)
styles.css                      — your hand-built stylesheet
styles-ai-generated.css         — AI-generated stylesheet from this spec
AI_Decision_Log_S02.md          — your completed Decision Log
```
