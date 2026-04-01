# Home + Projects Design Spec
**Date:** 2026-04-01
**Scope:** `index.html` (home), `projects.html`, four case study pages
**Stack:** Straight HTML/CSS, no build step, GitHub Pages

---

## Design System (existing — do not extend without explicit ask)

| Token | Value |
|---|---|
| `--blue` | `#005BEC` |
| `--text` | `#1a1a1a` |
| `--muted` | `#555` |
| `--light` | `#999` |
| `--border` | `#e8e8e8` |
| `--pad` | `80px` desktop / `24px` mobile (≤860px) |
| `--nav-h` | `72px` |
| Heading font | Syne Tactile (logo/wordmark only) |
| Body font | Inter 400/500/600 |
| Border radius | `4px` |
| Line height | `1.5` (body copy throughout) |

---

## Shared Patterns

### Nav
Sticky, white background, `border-bottom: 1px solid var(--border)`, height `--nav-h`.
- Left: `studio cartelli` in Syne Tactile, `--blue`, links to `index.html`
- Right: Projects · Services · About — Inter 500, `--muted`, active page gets `--text`

### Content wrapper
All content pages (Projects, Services, About, case studies) use:
```css
.content {
  max-width: 720px;
  margin: 0 auto;
  padding: var(--pad);
}
```
720px ≈ 72ch at 16px base — within the 68–88 character readability target.

### Section label
```css
.section-label {
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--blue);
  margin-bottom: 14px;
}
```

---

## Home Page (`index.html`)

### Layout
- Sticky nav on white (as above)
- Blue panel fills remaining viewport height (`height: calc(100vh - var(--nav-h))`)
- Panel interior: flexbox row, `align-items: center`, `padding: 0 var(--pad)`

### Blue panel — left column (flex: 1)
- **Headline:** `h1`, Inter 600, `clamp(1.75rem, 4vw, 2.5rem)`, white, `line-height: 1.15`
  - Copy: *"Enterprise-grade MVP design for technical founders."*
- **Value prop:** `p`, Inter 400, `1rem`, `rgba(255,255,255,0.75)`, `line-height: 1.5`, `margin-top: 12px`
  - Copy: *"Fixed-scope sprints, 2–4 weeks. You work directly with Patrick, not a rotating team."*
- **CTAs:** flex row, `gap: 12px`, `margin-top: 28px`
  - Primary: "View Projects" → `projects.html` — white background, `--blue` text, Inter 500, `0.875rem`, `padding: 12px 20px`, `border-radius: 4px`
  - Secondary: "Get in Touch" → `mailto:ciao@studiocartelli.com` — transparent bg, white border `1px solid rgba(255,255,255,0.5)`, white text

### Blue panel — right column (width: 180px, flex-shrink: 0)
- `border-left: 1px solid rgba(255,255,255,0.2)`, `padding-left: 28px`
- **Availability label:** section label style, `rgba(255,255,255,0.55)`
- **Availability value:** *"Taking select projects"* — Inter 600, `0.9375rem`, white
- **Services label:** section label style, `rgba(255,255,255,0.55)`, `margin-top: 20px`
- **Services value:** *"Design sprints / 2–4 weeks / $3K–$15K"* — Inter 400, `0.875rem`, `rgba(255,255,255,0.8)`, `line-height: 1.6`

### Mobile (≤860px)
Panel interior switches to `flex-direction: column`, stacked:
1. Headline + value prop + CTAs
2. Availability + services as a simple two-field block, `border-top: 1px solid rgba(255,255,255,0.2)`, `padding-top: 24px`, `margin-top: 24px`

---

## Projects Page (`projects.html`)

### Layout
Nav + `.content` wrapper (720px max-width, centered).

### Page header
Section label: "PROJECTS"

### Card list
Bordered list — `border-top: 1px solid var(--border)` before first card, each card has `border-bottom: 1px solid var(--border)`.

Each card is an `<a>` wrapping the card content (`display: block`, `text-decoration: none`, `padding: 20px 0`).

**Card structure (top to bottom):**
1. Client label — `.section-label` style, `margin-bottom: 6px`
2. Title — Inter 600, `1rem`, `--text`, `margin-bottom: 6px`
3. Problem framing — Inter 400, `0.875rem`, `--muted`, `line-height: 1.5`
4. Outcomes row — Inter 600, `0.75rem`, `--text`, `margin-top: 10px`, stats separated by ` · `

**Hover state:** `background: #f5f8ff` (light blue tint, stays in system)

**Cards (in order):**
| Title | Client | Problem (1 sentence) | Outcomes |
|---|---|---|---|
| Precision Alert Monitoring | Dataminr | Rigid alert configs forced 100,000+ security analysts to build workarounds, creating noise and missed threats. | 20% less noise · 65% faster config · 45% fewer tickets |
| Mission-Critical Trust | Dataminr | Security managers couldn't trust what the platform delivered — no preview, no visibility, no verification. | 250,000+ analysts · 40% adoption increase · 10,000+ accounts unblocked |
| Strategic Reporting at Scale | Vividly | CPG finance teams were exporting data daily because the platform couldn't support basic analysis. | Daily exports dropped to as-needed · 100% beta acceptance · 500 products, 800+ customers at <2s |
| The Check-In Problem | Gympass | Users weren't checking in, costing six figures annually — but the assumption of user forgetfulness was wrong. | First baseline metrics established · Phased strategy addressed root causes · Framework guided COVID reopening |
| Vividly Design System | Vividly | *(Pending — source material needed from Patrick)* | *(Pending)* |

---

## Case Study Pages

### Files
- `precision-alert-monitoring.html`
- `mission-critical-trust.html`
- `strategic-reporting.html`
- `check-in-problem.html`
- `vividly-design-system.html` *(pending)*

### Layout
Nav + `.content` wrapper (720px max-width).

### Structure (top to bottom)
1. `← Back to Projects` — small link, `--muted`, `font-size: 0.875rem`, `margin-bottom: 32px`
2. Page `h1` — case study title, Inter 600, `clamp(1.5rem, 3vw, 2rem)`, `--text`
3. Client subhead — Inter 400, `1rem`, `--muted`, `margin-top: 4px`
4. Three sections with `.section-label` + content:
   - **PROBLEM** — 2–4 sentences. What was broken and who felt it.
   - **INSIGHT** — 1–3 sentences. The reframe that changed direction.
   - **OUTCOME** — Stats list or short paragraph.
5. Bottom CTA — *"Working on something similar? [Get in touch](mailto:ciao@studiocartelli.com)"* — inline link, `--blue`, no button

### Section spacing
`margin-top: 40px` between sections.

---

## Files to Create / Modify

| File | Action |
|---|---|
| `index.html` | Rewrite (currently placeholder only) |
| `projects.html` | Create new |
| `precision-alert-monitoring.html` | Create new |
| `mission-critical-trust.html` | Create new |
| `strategic-reporting.html` | Create new |
| `check-in-problem.html` | Create new |
| `about.html` | Update nav labels + line-height + `.content` wrapper |

---

## Deferred / Follow-up

- **Vividly Design System case study** — Patrick to provide source material and reframe angle before page is written
- **Services page** — separate spec/build
- **Calendly integration** — replace `mailto:` CTAs when link is available
- **Headshot** — replace placeholder in `about.html`
- **patcartelli.com "About Patrick" link** — confirm placement (About page nav or footer)
- **`work.html`** — currently linked from `about.html` nav; rename to `projects.html` and update all references
