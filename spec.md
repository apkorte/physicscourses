# Spec: physicscourses.co.uk Landing Page

---

## SECTION 1: SPEC

**One-line purpose**
A lightweight landing page at physicscourses.co.uk that establishes credibility and routes visitors to physicsandmathscourses.com to book A-level revision courses.

**Users and use cases**
- As a student searching for A-level Physics revision, I want to quickly understand what's on offer and who teaches it so I can decide whether to visit the main site.
- As a parent researching revision courses for their child, I want to see the tutor's credentials and course format so I feel confident enough to click through.
- As a search engine crawler, I want clear structured content so the page ranks for relevant UK A-level revision queries.

**Requirements**
1. Page must display the tutor's name and credentials (Oxford First, Imperial PhD).
2. Page must describe the course format: small group, online via Zoom.
3. Page must name the subjects offered: Maths, Physics, Further Maths.
4. Page must name the course timing: Easter and summer intensive.
5. Page must state that all major exam boards are covered.
6. Page must include at least one clearly labelled call-to-action linking to physicsandmathscourses.com.
7. Page must be a single self-contained `index.html` file.
8. Page must load Google Fonts via a standard `<link>` tag — no other external dependencies.
9. Page must be mobile-responsive with no horizontal scroll on screens ≥320 px wide.
10. Page must use `#0077bb` as the primary brand colour.
11. Page must include a `<title>`, `meta description`, and `<h1>` optimised for "A-level Physics revision courses UK" and related terms.
12. Page must include `canonical` pointing to `https://physicscourses.co.uk/`.

**Edge cases**
- Visitor lands on the page with JavaScript disabled: all content and the CTA must be fully accessible — no JS required.
- Visitor uses a screen reader: heading hierarchy, link text, and alt attributes must be meaningful.
- Visitor is on a slow mobile connection: no render-blocking resources beyond the single Google Fonts `<link>`.
- physicsandmathscourses.com is down: the landing page itself must still load and display all content; the CTA is just a hyperlink, so this is inherently handled.

**Acceptance criteria**

```
Given a visitor loads the page in a modern browser
When the page finishes rendering
Then the tutor's name, credentials, subjects, format, and CTA link are all visible above the fold on a 375 px wide screen

Given a visitor clicks the primary CTA button
When the click is registered
Then the browser navigates to https://www.physicsandmathscourses.com in the same tab

Given a search engine crawls the page
When it reads the <head>
Then it finds a <title> containing "A-level" and "Physics", a meta description under 160 characters, and a canonical tag

Given a visitor views the page with CSS disabled
When the page renders
Then all text content is readable in logical reading order

Given a visitor resizes the browser to 320 px wide
When the layout reflows
Then no element overflows horizontally and all text remains legible
```

---

## SECTION 2: PLAN

**Stack and architecture**
Pure static HTML — single `index.html` file. Inline `<style>` block for all CSS. No JavaScript. One external resource: Google Fonts via `<link rel="preconnect">` + `<link rel="stylesheet">`. Deployed via GitHub Pages with a custom domain CNAME. No build step.

**Data model changes**
None. All content is hardcoded in the HTML.

**API contracts**
None. The only outbound link is the CTA href to `https://www.physicsandmathscourses.com`.

**Patterns to follow**
Greenfield single file. Semantic HTML5 with a single-column layout optimised for readability.

Structural sections in order:
1. `<head>` — meta, title, canonical, OG tags, Google Fonts link, inline `<style>`
2. `<header>` — site name / logo text
3. `<main>`
   - Hero: headline, sub-headline, primary CTA button
   - Credentials block: tutor name, Oxford/Imperial credentials
   - Course details: subjects, format, timing, exam boards
   - Secondary CTA
4. `<footer>` — copyright, link to main site

**Testing strategy**
Manual only (static file):
- Open in Chrome, Firefox, Safari — verify layout at 375 px, 768 px, 1280 px.
- Run through Lighthouse for Performance, Accessibility, SEO — target ≥90 on all.
- Validate HTML at validator.w3.org.
- Check all links resolve.

**Security and performance constraints**
- No forms, no user input, no cookies — no data-security surface.
- Google Fonts loaded with `rel="preconnect"` + `display=swap` to avoid render-blocking.
- No images — typographic design only.
- `<meta name="viewport" content="width=device-width, initial-scale=1">` required.

---

## SECTION 3: TASKS

## Task 1: HTML scaffold and `<head>`

**What to build:** The complete `<head>` section including charset, viewport, title, meta description, canonical, Open Graph tags, and Google Fonts link. Also the outermost `<body>` wrapper with empty section placeholders.
**Files likely affected:** `index.html` (create)
**Acceptance criteria:**
1. `<title>` contains the string "A-level Physics & Maths Revision Courses" or equivalent.
2. `meta description` is present, under 160 characters, mentions Physics, Maths, online, and UK.
3. `<link rel="canonical" href="https://physicscourses.co.uk/">` is present.
**Dependencies:** none

---

## Task 2: Inline CSS — layout, typography, colour system

**What to build:** Full inline `<style>` block covering: CSS custom properties (`--brand: #0077bb`), reset, typography scale, single-column centred layout, responsive breakpoints, button styles, and section spacing.
**Files likely affected:** `index.html` (style block)
**Acceptance criteria:**
1. Page renders without horizontal scroll at 320 px, 375 px, 768 px, and 1280 px viewport widths.
2. Primary brand colour `#0077bb` is used on the CTA button and at least one heading accent.
3. Body text is legible at default zoom — minimum 1rem / 16 px equivalent.
**Dependencies:** Task 1

---

## Task 3: Hero section and primary CTA

**What to build:** `<header>` and hero `<section>` containing: site name, a punchy `<h1>` headline, a one-sentence sub-headline describing the offer, and a prominent `<a>` styled as a button linking to `https://www.physicsandmathscourses.com`.
**Files likely affected:** `index.html`
**Acceptance criteria:**
1. `<h1>` is present and unique on the page.
2. CTA link href resolves to `https://www.physicsandmathscourses.com` and has descriptive link text (not "click here").
3. Hero content is the first visible content on every viewport width tested.
**Dependencies:** Task 2

---

## Task 4: Credentials and trust section

**What to build:** A section naming Dr Anthony Korte, listing his Oxford First Class degree and Imperial College PhD in Theoretical Physics, and communicating why this matters to the audience.
**Files likely affected:** `index.html`
**Acceptance criteria:**
1. "Dr Anthony Korte", "Oxford", and "Imperial College" all appear as visible text.
2. Section has a logical heading (`<h2>`) within the page's heading hierarchy.
3. Content is readable on mobile without truncation.
**Dependencies:** Task 3

---

## Task 5: Course details section

**What to build:** A section covering: subjects (Maths, Physics, Further Maths), format (small group, online via Zoom), timing (Easter intensive, summer intensive), and exam boards (AQA, OCR, Edexcel — plus "all major boards").
**Files likely affected:** `index.html`
**Acceptance criteria:**
1. All three subjects are named explicitly.
2. "Easter" and "summer" both appear as visible text describing course timing.
3. At least three exam board names are present.
**Dependencies:** Task 3

---

## Task 6: Secondary CTA and footer

**What to build:** A closing CTA section repeating the link to physicsandmathscourses.com with brief supporting copy, and a `<footer>` with copyright notice and the main site URL as a plain text link.
**Files likely affected:** `index.html`
**Acceptance criteria:**
1. A second link to `https://www.physicsandmathscourses.com` is present below the course details.
2. `<footer>` is present and contains a copyright line.
3. Page passes W3C HTML validation with no errors.
**Dependencies:** Tasks 4, 5

---

**Review checkpoint:** Before handing to an agent, confirm: (a) whether the CTA should open in a new tab, (b) whether a tutor headshot image is available to include, and (c) whether you want the Google Font chosen by the agent or have a specific preference.

---

## Assumptions to review

1. Canonical domain is non-www (`https://physicscourses.co.uk/`) — **Impact: HIGH**
   Correct this if: GitHub Pages CNAME is configured for `www.physicscourses.co.uk` instead.

2. CTA opens in the same tab — **Impact: MEDIUM**
   Correct this if: you prefer `target="_blank"` so visitors don't leave the page entirely.

3. No tutor headshot available — typographic design only — **Impact: MEDIUM**
   Correct this if: a photo exists; it would significantly strengthen the trust section.

4. One Google Font family, two weights (400 + 600) — **Impact: LOW**
   Correct this if: you have a brand font already in use on physicsandmathscourses.com that should match.

5. Exam boards listed are AQA, OCR, Edexcel — **Impact: LOW**
   Correct this if: additional boards (WJEC, CIE, etc.) should be named explicitly.
