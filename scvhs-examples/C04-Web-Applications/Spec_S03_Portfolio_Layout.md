# Spec_S03_Portfolio_Layout.md

**Author:** [Your name]
**Sprint:** 3 — Design Effective Web Layouts with UI/UX Principles
**Date:** [Date]
**SCVHS Mode:** Hybrid / Generate-then-Explain — you write this spec, an AI tool constructs the Tailwind + ShadCN layout, you read the output construct by construct, fill your Decision Log, fix defects, and ship the corrected AI output. See the Comprehension Primitive section before directing the AI.
**Base:** `portfolio.html` from Sprint 1 — HTML structure is preserved. Sprint 2 stylesheet is replaced entirely by Tailwind utility classes.

---

## Purpose

Make the portfolio responsive across mobile, tablet, and desktop using Tailwind CSS and ShadCN/UI components. Replace the Sprint 2 hand-written stylesheet entirely. All styling must come from Tailwind utility classes.

---

## Figma Source Values
*(Read these from the Figma Inspect panel. Record which class maps to which value in your Decision Log.)*

| Value              | Source in Figma         | Tailwind class you will use |
|--------------------|-------------------------|-----------------------------|
| Spacing unit       | 8px base                | Tailwind spacing scale (p-2 = 8px, p-4 = 16px, etc.) |
| Max content width  | 1024px                  | `max-w-4xl`                 |
| Primary colour     | #2563EB                 | `text-blue-600`, `bg-blue-600` |
| Background         | #FFFFFF                 | `bg-white`                  |
| Surface (cards)    | #F8FAFC                 | `bg-slate-50`               |
| Text               | #1A1A1A                 | `text-gray-900`             |
| Muted              | #6B7280                 | `text-gray-500`             |

---

## Breakpoints
*(Mobile-first — build up from default, never override from desktop down)*

| Prefix | Minimum width | Layout change                        |
|--------|---------------|--------------------------------------|
| default | < 640px      | Single column, nav hidden, hero stacked |
| `sm:`  | ≥ 640px       | Projects 2-column, hero switches to row |
| `lg:`  | ≥ 1024px      | Projects 3-column                    |

---

## ShadCN/UI Components
*(All 5 must appear in the final page with correct prop API)*

| # | Component   | Used for                              |
|---|-------------|---------------------------------------|
| 1 | `Button`    | Hero CTA ("View Projects") and project links |
| 2 | `Card`      | Wraps each project article (CardHeader, CardContent, CardFooter) |
| 3 | `Badge`     | Tech stack tags inside each project card |
| 4 | `Separator` | Horizontal divider between major sections |
| 5 | `Avatar`    | Profile photo in hero section         |

---

## Layout by Section

### 1. Hero (`<header>` element)

| Breakpoint | Layout |
|------------|--------|
| Default    | Stacked — Avatar above name, nav links below |
| `sm:`      | Row — Avatar left, name and nav right |

Tailwind classes:
```
header:   flex flex-col sm:flex-row items-center gap-6 p-6 lg:p-10 bg-gray-900 text-white
h1:       text-3xl sm:text-4xl font-bold text-white
tagline:  text-sm text-gray-400 mt-1
```
ShadCN: `Avatar` for profile photo
ShadCN: `Button variant="outline"` for "Download CV" link

---

### 2. Navigation (`<nav>` element)

| Breakpoint | Layout          |
|------------|-----------------|
| Default    | Hidden (mobile) |
| `md:`      | Visible row     |

Tailwind classes:
```
nav:   hidden md:flex gap-6
nav a: text-white hover:underline text-sm font-medium
```

---

### 3. Main (`<main>` element)

```
main: max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-10
```

---

### 4. About (`<section>` element)

Single column at all breakpoints.

```
section: space-y-4 pb-10
h2:      text-2xl font-semibold mb-4
```
ShadCN: `Separator` below section

---

### 5. Projects (`<section>` element)

| Breakpoint | Columns |
|------------|---------|
| Default    | 1       |
| `sm:`      | 2       |
| `lg:`      | 3       |

```
section:       space-y-6
h2:            text-2xl font-semibold mb-6
projects grid: grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6
```

Each project — ShadCN `Card`:
- `CardHeader`: `<h3>` project name — `text-lg font-semibold`
- `CardContent`: `<p>` description + `Badge` per tech tag
- `CardFooter`: `Button variant="link"` for project link

ShadCN: `Separator` below section

---

### 6. Contact (`<section>` element)

Single column at all breakpoints.

```
section: py-10 space-y-3
h2:      text-2xl font-semibold mb-4
links:   text-blue-600 hover:underline
```

---

### 7. Footer (`<footer>` element)

```
footer: bg-gray-100 text-center text-sm text-gray-500 py-6
```

---

## Comprehension Primitive
*(Hand-write this before giving the spec to an AI tool — proves you can read Grid)*

Create a file called `scratch_grid.html`. Write this CSS by hand:

```css
.grid-3col {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}
```

Place 3 divs inside a `.grid-3col` container and confirm the 3-column layout in the browser.
Commit this file alongside the spec. It builds your Grid mental model before CONSTRUCT, and it also
gives the AI tool a concrete example of the Grid pattern to follow.

---

## Acceptance Criteria
*(This list is your VALIDATE checklist — check every item before submitting)*

**Tailwind**
- Zero custom CSS: no `.css` file, no `<style>` block, no inline `style=` attribute
- Zero arbitrary values: no `w-[437px]`, `h-[200px]`, or similar
- All spacing uses Tailwind scale (`p-4`, `gap-6`, `mt-8`, etc.)
- All font sizes use Tailwind type scale (`text-sm`, `text-base`, `text-xl`, etc.)

**Responsive** *(verify in DevTools Device Mode at each width)*
- Default (< 640px): single-column projects, nav hidden, hero stacked
- `sm:` (640px): projects switch to 2 columns, hero switches to row
- `lg:` (1024px): projects switch to 3 columns
- Breakpoints are additive and mobile-first: `sm:` adds to default, never overrides it

**ShadCN/UI**
- All 5 components present: `Button`, `Card`, `Badge`, `Separator`, `Avatar`
- Each component uses the correct prop (`variant=`, `size=`, etc.)
- `Card` uses `CardHeader`, `CardContent`, `CardFooter` slots correctly

**Figma values** *(minimum 3 — record each in Decision Log)*
- For each: Figma source value → Tailwind class used → where applied in code

**Contrast** *(WCAG AA — verify in DevTools Accessibility panel)*
- White text on `bg-gray-900` header: ≥ 4.5:1
- Body text `#1A1A1A` on white: ≥ 4.5:1
- Badge text on badge background: ≥ 4.5:1

---

