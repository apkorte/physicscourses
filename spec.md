# Spec: physicscourses.co.uk Landing Page

---

## SECTION 1: SPEC

**One-line purpose**
A lightweight landing page at physicscourses.co.uk laser-focused on A-level Physics revision, that establishes credibility and routes visitors to physicsandmathscourses.com to book. Maths courses have their own domain (alevelmathsonline.co.uk).

**Users and use cases**
- As a student searching for A-level Physics revision, I want to quickly understand what's on offer and who teaches it so I can decide whether to visit the main site.
- As a parent researching Physics revision courses for their child, I want to see the tutor's credentials and course format so I feel confident enough to click through.
- As a search engine crawler, I want clear structured content and FAQ schema so the page ranks for relevant UK A-level Physics revision queries.

**Requirements**
1. Page must be laser-focused on Physics — Maths is de-emphasised in hero and body copy.
2. Page must display the tutor's name and all three credentials (Oxford First, UCL MSc, Imperial PhD).
3. Page must describe the course format: small group, online via Zoom.
4. Page must name all subjects offered but lead with Physics: A-level Physics, Mathematics, Further Mathematics.
5. Page must name course timing: Easter, summer, and Christmas intensive.
6. Page must list Physics exam boards covered: AQA, OCR A, OCR B, Edexcel, WJEC Eduqas.
7. Page must include at least one clearly labelled CTA linking to physicsandmathscourses.com.
8. Page must be a single self-contained `index.html` file with inline CSS — no external dependencies.
9. Page must be mobile-responsive: portrait orientation fix, high-DPI fix, no horizontal scroll ≥320px.
10. Page must use `#0077bb` as the primary brand colour and system font stack.
11. `<title>` must be "A-level Physics Revision Courses | physicscourses.co.uk".
12. `<h1>` must be "A-level Physics Revision Courses".
13. Page must include `canonical` pointing to `https://physicscourses.co.uk/`.
14. Page must include a FAQ section (6 questions) after the course detail cards.
15. Footer must include subtle cross-links to alevelmathsonline.co.uk and oxfordpat.co.uk.
16. JSON-LD must include: Person (with all three hasCredential), one Physics Course (url = https://physicscourses.co.uk/), EducationalOrganization, FAQPage.

**Confirmed decisions**
- CTA opens in a new tab (`target="_blank" rel="noopener noreferrer"`)
- No headshot — typographic design only
- System font stack: "Helvetica Neue", Helvetica, Arial, sans-serif — no Google Fonts
- hero.jpeg background image with dark navy overlay
- favicon.ico referenced in head
- sitemap.xml referenced in head
- All CTAs link to https://physicsandmathscourses.com (no www)

**Edge cases**
- Visitor lands with JavaScript disabled: all content and CTAs fully accessible.
- Visitor uses a screen reader: heading hierarchy, link text, and alt attributes must be meaningful.
- physicsandmathscourses.com is down: landing page loads and displays all content independently.

---

## SECTION 2: PLAN

**Stack and architecture**
Pure static HTML — single `index.html`. Inline `<style>` block. No JavaScript. No external dependencies except favicon.ico and hero.jpeg in the same directory. Deployed via GitHub Pages with custom domain CNAME.

**Structural sections in order:**
1. `<head>` — meta, title, canonical, OG, sitemap link, favicon, JSON-LD (Person, Course, EducationalOrganization, FAQPage), inline `<style>`
2. `.brand-bar` — 4px brand colour rule
3. `<header>` — site name + "Book a place" nav link
4. `<main>`
   - Hero: Physics-focused headline, sub-headline, primary CTA
   - Credentials: Dr Anthony Korte, three qualifications, body paragraph
   - Course details: 4-card grid (Subjects, Format, When, Physics exam boards)
   - FAQ: 6 questions with schema-matching markup
5. Secondary CTA band
6. `<footer>` — copyright, cross-links to alevelmathsonline.co.uk + oxfordpat.co.uk, Privacy Policy

**JSON-LD schemas:**
- Person: Dr Anthony Korte, 3× hasCredential, alumniOf Oxford/UCL/Imperial
- Course: A-level Physics Revision Course, url = https://physicscourses.co.uk/
- EducationalOrganization: sameAs https://physicsandmathscourses.com
- FAQPage: 6 Q&A pairs matching the FAQ section

**CSS architecture:**
- Design tokens in :root (--brand, --ink, etc.)
- html { font-size: 16px } base; body text elements set to explicit 18px
- -webkit-text-size-adjust: 100% on both html and body
- Retina + max-width: 768px query: body/p/li/dd/dt to 20px
- Portrait + max-width: 500px query: html font-size 18px
- max-width: 600px: layout collapses (single column cards, stacked CTA, hide nav button)

---

## SECTION 3: TASKS

## Task 1: Focus change — title, meta, OG, hero copy
- `<title>`: "A-level Physics Revision Courses | physicscourses.co.uk"
- `<meta description>`: Physics-only focus, under 160 chars
- OG title/description: Physics-only
- `<h1>`: "A-level Physics Revision Courses"
- Hero kicker: remove Maths references
- Hero sub: Physics-focused, mention Maths only as supporting subject

## Task 2: Schema fixes
- Person hasCredential: add MSc with Distinction in Mathematical Modelling, UCL
- Person alumniOf: add University College London
- Physics Course url: https://physicscourses.co.uk/
- Remove Maths and Further Maths Course schemas (page is Physics-focused)
- Add FAQPage JSON-LD matching exact FAQ section Q&As

## Task 3: FAQ section
Add after course detail cards. Six questions:
1. "What is an A-level Physics revision course?"
2. "Which exam boards do you cover?"
3. "How does online Physics tuition work?"
4. "When are the Easter and summer Physics revision courses?"
5. "What makes these Physics courses different?"
6. "Is the course suitable for Year 12 and Year 13?"

Style: clean accordion-free list (no JS), question as `<h3>`, answer as `<p>`.

## Task 4: Footer cross-links
Add a subtle second row or inline line in footer:
- "A-level Maths courses: alevelmathsonline.co.uk"
- "ESAT / Oxford PAT preparation: oxfordpat.co.uk"
No "coming soon" or status labels.

---

## Confirmed assumptions
1. Canonical: non-www `https://physicscourses.co.uk/`
2. CTAs open in new tab
3. No headshot — typographic only
4. System fonts only — no Google Fonts
5. Physics exam boards: AQA, OCR A, OCR B, Edexcel, WJEC Eduqas
6. Maths has its own domain: alevelmathsonline.co.uk
7. ESAT prep: oxfordpat.co.uk
