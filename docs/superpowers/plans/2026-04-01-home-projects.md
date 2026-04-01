# Home + Projects Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the home page and projects section of studiocartelli.com — index.html, projects.html, four case study pages, and nav/style updates to about.html.

**Architecture:** Straight HTML/CSS, no build step, no framework. Each page is self-contained with its own `<style>` block. Nav markup is duplicated across pages (intentional — find-and-replace is the update path). Shared patterns (CSS variables, nav, .content wrapper, .section-label) are identical across all files. GitHub Pages serves files directly from main branch.

**Tech Stack:** HTML5, CSS3, Inter (Google Fonts), Syne Tactile (Google Fonts), GitHub Pages

**Note on testing:** No automated test framework. Verification steps are browser-based checklists against the spec. Each task ends with an explicit checklist to confirm before committing.

---

## File Map

| File | Action | Responsibility |
|---|---|---|
| `index.html` | Rewrite | Home page: nav + blue hero panel with split layout |
| `projects.html` | Create | Project card list, routes to case study pages |
| `precision-alert-monitoring.html` | Create | Case study: Dataminr alert monitoring |
| `mission-critical-trust.html` | Create | Case study: Dataminr content management |
| `strategic-reporting.html` | Create | Case study: Vividly reporting |
| `check-in-problem.html` | Create | Case study: Gympass check-in |
| `about.html` | Modify | Update nav labels, line-height, add .content wrapper |
| `.gitignore` | Modify | Add `.superpowers/` entry |

---

## Shared CSS Reference

Every page uses this identical CSS for nav, content wrapper, and section labels. Copy it exactly — do not vary between files.

```css
* { margin: 0; padding: 0; box-sizing: border-box; }

:root {
  --blue: #005BEC;
  --text: #1a1a1a;
  --muted: #555;
  --light: #999;
  --border: #e8e8e8;
  --pad: 80px;
  --nav-h: 72px;
}

html, body { min-height: 100%; }

body {
  background: white;
  font-family: 'Inter', sans-serif;
  color: var(--text);
}

nav {
  position: sticky;
  top: 0;
  z-index: 100;
  background: white;
  border-bottom: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: var(--nav-h);
  padding: 0 var(--pad);
}

.logo {
  font-family: 'Syne Tactile', sans-serif;
  font-size: 1.25rem;
  color: var(--blue);
  text-decoration: none;
}

.nav-links {
  display: flex;
  gap: 32px;
  list-style: none;
}

.nav-links a {
  font-size: 0.875rem;
  font-weight: 500;
  color: var(--muted);
  text-decoration: none;
}

.nav-links a.active { color: var(--text); }

.content {
  max-width: 720px;
  margin: 0 auto;
  padding: var(--pad);
}

.section-label {
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--blue);
  margin-bottom: 14px;
}

@media (max-width: 860px) {
  :root { --pad: 24px; }
  nav { padding: 0 24px; }
  .nav-links { gap: 20px; }
}
```

Shared nav HTML (set `class="active" aria-current="page"` on the link matching the current page):

```html
<nav>
  <a href="index.html" class="logo">studio cartelli</a>
  <ul class="nav-links">
    <li><a href="projects.html">Projects</a></li>
    <li><a href="services.html">Services</a></li>
    <li><a href="about.html">About</a></li>
  </ul>
</nav>
```

---

## Task 1: Housekeeping — .gitignore

**Files:**
- Modify: `.gitignore` (create if absent)

- [ ] **Step 1: Check if .gitignore exists**

```bash
cat /Users/pcartelli/patcartelli.github.io/.gitignore
```

- [ ] **Step 2: Add .superpowers/ entry**

If the file exists, append. If not, create it. The file should contain at minimum:

```
.superpowers/
```

- [ ] **Step 3: Commit**

```bash
cd /Users/pcartelli/patcartelli.github.io
git add .gitignore
git commit -m "chore: ignore brainstorm session files"
```

---

## Task 2: Home page (`index.html`)

**Files:**
- Rewrite: `index.html`

- [ ] **Step 1: Replace index.html with the following**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Studio Cartelli — Enterprise-grade MVP design for technical founders. Fixed-scope design sprints, 2–4 weeks.">
  <title>Studio Cartelli</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Syne+Tactile&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --blue: #005BEC;
      --text: #1a1a1a;
      --muted: #555;
      --light: #999;
      --border: #e8e8e8;
      --pad: 80px;
      --nav-h: 72px;
    }

    html, body { height: 100%; }

    body {
      background: white;
      font-family: 'Inter', sans-serif;
      color: var(--text);
      display: flex;
      flex-direction: column;
    }

    nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: white;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: var(--nav-h);
      padding: 0 var(--pad);
      flex-shrink: 0;
    }

    .logo {
      font-family: 'Syne Tactile', sans-serif;
      font-size: 1.25rem;
      color: var(--blue);
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 32px;
      list-style: none;
    }

    .nav-links a {
      font-size: 0.875rem;
      font-weight: 500;
      color: var(--muted);
      text-decoration: none;
    }

    .nav-links a.active { color: var(--text); }

    main {
      background: var(--blue);
      flex: 1;
      display: flex;
      align-items: center;
      padding: 0 var(--pad);
      border-radius: 4px;
      margin: 0 var(--pad) var(--pad);
    }

    .hero {
      display: flex;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      gap: 48px;
    }

    .hero-left { flex: 1; }

    h1 {
      font-size: clamp(1.75rem, 4vw, 2.5rem);
      font-weight: 600;
      color: white;
      line-height: 1.15;
      letter-spacing: -0.02em;
    }

    .value-prop {
      font-size: 1rem;
      color: rgba(255, 255, 255, 0.75);
      line-height: 1.5;
      margin-top: 12px;
    }

    .cta-row {
      display: flex;
      gap: 12px;
      margin-top: 28px;
    }

    .btn-primary {
      background: white;
      color: var(--blue);
      font-family: 'Inter', sans-serif;
      font-size: 0.875rem;
      font-weight: 500;
      padding: 12px 20px;
      border-radius: 4px;
      text-decoration: none;
      transition: opacity 0.15s;
    }

    .btn-primary:hover { opacity: 0.88; }

    .btn-secondary {
      border: 1px solid rgba(255, 255, 255, 0.5);
      color: white;
      font-family: 'Inter', sans-serif;
      font-size: 0.875rem;
      font-weight: 500;
      padding: 12px 20px;
      border-radius: 4px;
      text-decoration: none;
      transition: opacity 0.15s;
    }

    .btn-secondary:hover { opacity: 0.75; }

    .hero-right {
      width: 180px;
      flex-shrink: 0;
      border-left: 1px solid rgba(255, 255, 255, 0.2);
      padding-left: 28px;
    }

    .status-label {
      font-size: 0.7rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: rgba(255, 255, 255, 0.55);
      margin-bottom: 6px;
    }

    .status-value {
      font-size: 0.9375rem;
      font-weight: 600;
      color: white;
      line-height: 1.3;
    }

    .services-block { margin-top: 20px; }

    .services-value {
      font-size: 0.875rem;
      color: rgba(255, 255, 255, 0.8);
      line-height: 1.6;
    }

    @media (max-width: 860px) {
      :root { --pad: 24px; }
      nav { padding: 0 24px; }
      .nav-links { gap: 20px; }
      main { margin: 0 24px 24px; padding: var(--pad); }
      .hero { flex-direction: column; gap: 24px; align-items: flex-start; }
      .hero-right {
        width: 100%;
        border-left: none;
        border-top: 1px solid rgba(255, 255, 255, 0.2);
        padding-left: 0;
        padding-top: 24px;
        display: flex;
        gap: 32px;
      }
      .services-block { margin-top: 0; }
    }
  </style>
</head>
<body>
  <nav>
    <a href="index.html" class="logo">studio cartelli</a>
    <ul class="nav-links">
      <li><a href="projects.html">Projects</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
    </ul>
  </nav>

  <main>
    <div class="hero">
      <div class="hero-left">
        <h1>Enterprise-grade MVP design for technical founders.</h1>
        <p class="value-prop">Fixed-scope sprints, 2–4 weeks. You work directly with Patrick, not a rotating team.</p>
        <div class="cta-row">
          <a href="projects.html" class="btn-primary">View Projects</a>
          <a href="mailto:ciao@studiocartelli.com" class="btn-secondary">Get in Touch</a>
        </div>
      </div>
      <div class="hero-right">
        <div>
          <div class="status-label">Availability</div>
          <div class="status-value">Taking select projects</div>
        </div>
        <div class="services-block">
          <div class="status-label">Services</div>
          <div class="services-value">Design sprints<br>2–4 weeks<br>$3K–$15K</div>
        </div>
      </div>
    </div>
  </main>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

Open `index.html` directly in a browser (or `open index.html` from terminal). Check:

- [ ] Nav: white background, sticky, "studio cartelli" in blue Syne Tactile left, Projects/Services/About right in Inter
- [ ] Blue panel fills viewport below nav, no white gap at bottom
- [ ] Headline renders in white Inter, not Syne Tactile
- [ ] Value prop is slightly transparent white, line-height visually comfortable
- [ ] Two CTAs render: white "View Projects" button + ghost "Get in Touch"
- [ ] Right column: vertical divider, "Availability" + "Taking select projects" + "Services" block below
- [ ] Resize to under 860px: layout stacks, hero-right becomes horizontal row at bottom of panel

- [ ] **Step 3: Commit**

```bash
cd /Users/pcartelli/patcartelli.github.io
git add index.html
git commit -m "feat: build home page with blue hero panel and split layout"
```

---

## Task 3: Projects page (`projects.html`)

**Files:**
- Create: `projects.html`

- [ ] **Step 1: Create projects.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Studio Cartelli — Selected projects in enterprise B2B SaaS product design.">
  <title>Projects — Studio Cartelli</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Syne+Tactile&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --blue: #005BEC;
      --text: #1a1a1a;
      --muted: #555;
      --light: #999;
      --border: #e8e8e8;
      --pad: 80px;
      --nav-h: 72px;
    }

    html, body { min-height: 100%; }

    body {
      background: white;
      font-family: 'Inter', sans-serif;
      color: var(--text);
    }

    nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: white;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: var(--nav-h);
      padding: 0 var(--pad);
    }

    .logo {
      font-family: 'Syne Tactile', sans-serif;
      font-size: 1.25rem;
      color: var(--blue);
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 32px;
      list-style: none;
    }

    .nav-links a {
      font-size: 0.875rem;
      font-weight: 500;
      color: var(--muted);
      text-decoration: none;
    }

    .nav-links a.active { color: var(--text); }

    .content {
      max-width: 720px;
      margin: 0 auto;
      padding: var(--pad);
    }

    .section-label {
      font-size: 0.7rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--blue);
      margin-bottom: 14px;
    }

    .card-list {
      border-top: 1px solid var(--border);
    }

    .card {
      display: block;
      text-decoration: none;
      color: inherit;
      padding: 20px 0;
      border-bottom: 1px solid var(--border);
      border-radius: 4px;
      transition: background 0.15s, padding 0.15s;
    }

    .card:hover {
      background: #f5f8ff;
      padding-left: 12px;
      padding-right: 12px;
      margin-left: -12px;
      margin-right: -12px;
    }

    .card-client {
      font-size: 0.7rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--blue);
      margin-bottom: 6px;
    }

    .card-title {
      font-size: 1rem;
      font-weight: 600;
      color: var(--text);
      margin-bottom: 6px;
    }

    .card-problem {
      font-size: 0.875rem;
      color: var(--muted);
      line-height: 1.5;
    }

    .card-outcomes {
      font-size: 0.75rem;
      font-weight: 600;
      color: var(--text);
      margin-top: 10px;
    }

    @media (max-width: 860px) {
      :root { --pad: 24px; }
      nav { padding: 0 24px; }
      .nav-links { gap: 20px; }
    }
  </style>
</head>
<body>
  <nav>
    <a href="index.html" class="logo">studio cartelli</a>
    <ul class="nav-links">
      <li><a href="projects.html" class="active" aria-current="page">Projects</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
    </ul>
  </nav>

  <div class="content">
    <div class="section-label">Projects</div>
    <div class="card-list">

      <a href="precision-alert-monitoring.html" class="card">
        <div class="card-client">Dataminr</div>
        <div class="card-title">Precision Alert Monitoring</div>
        <div class="card-problem">Rigid alert configs forced 100,000+ security analysts to build workarounds, creating noise and missed threats.</div>
        <div class="card-outcomes">20% less noise · 65% faster config · 45% fewer tickets</div>
      </a>

      <a href="mission-critical-trust.html" class="card">
        <div class="card-client">Dataminr</div>
        <div class="card-title">Mission-Critical Trust</div>
        <div class="card-problem">Security managers couldn't trust what the platform delivered: no preview, no visibility, no verification.</div>
        <div class="card-outcomes">250,000+ analysts · 40% adoption increase · 10,000+ accounts unblocked</div>
      </a>

      <a href="strategic-reporting.html" class="card">
        <div class="card-client">Vividly</div>
        <div class="card-title">Strategic Reporting at Scale</div>
        <div class="card-problem">CPG finance teams were exporting data daily because the platform couldn't support basic analysis.</div>
        <div class="card-outcomes">Daily exports dropped to as-needed · 100% beta acceptance · 500 products, 800+ customers at under 2s</div>
      </a>

      <a href="check-in-problem.html" class="card">
        <div class="card-client">Gympass</div>
        <div class="card-title">The Check-In Problem</div>
        <div class="card-problem">Users weren't checking in, costing six figures annually, but the assumption of user forgetfulness was wrong.</div>
        <div class="card-outcomes">First baseline metrics established · Phased strategy addressed root causes · Framework guided COVID reopening</div>
      </a>

    </div>
  </div>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

- [ ] "Projects" nav link is dark (`--text`), others are muted
- [ ] Content is centered, noticeably narrower than the full browser window on wide screens
- [ ] Section label "PROJECTS" in small blue uppercase above the list
- [ ] Four cards render with client label, title, problem sentence, outcome stats
- [ ] Hovering a card shows light blue tint background
- [ ] Clicking a card navigates to a 404 (expected — case study pages not built yet)
- [ ] Resize to under 860px: content fills width with 24px gutters

- [ ] **Step 3: Commit**

```bash
cd /Users/pcartelli/patcartelli.github.io
git add projects.html
git commit -m "feat: build projects page with card list"
```

---

## Task 4: Case study — Precision Alert Monitoring

**Files:**
- Create: `precision-alert-monitoring.html`

- [ ] **Step 1: Create precision-alert-monitoring.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Precision Alert Monitoring — Studio Cartelli case study. 20% alert noise reduction, 65% faster configuration for 100,000+ security analysts.">
  <title>Precision Alert Monitoring — Studio Cartelli</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Syne+Tactile&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --blue: #005BEC;
      --text: #1a1a1a;
      --muted: #555;
      --light: #999;
      --border: #e8e8e8;
      --pad: 80px;
      --nav-h: 72px;
    }

    html, body { min-height: 100%; }

    body {
      background: white;
      font-family: 'Inter', sans-serif;
      color: var(--text);
    }

    nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: white;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: var(--nav-h);
      padding: 0 var(--pad);
    }

    .logo {
      font-family: 'Syne Tactile', sans-serif;
      font-size: 1.25rem;
      color: var(--blue);
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 32px;
      list-style: none;
    }

    .nav-links a {
      font-size: 0.875rem;
      font-weight: 500;
      color: var(--muted);
      text-decoration: none;
    }

    .nav-links a.active { color: var(--text); }

    .content {
      max-width: 720px;
      margin: 0 auto;
      padding: var(--pad);
    }

    .back-link {
      display: inline-block;
      font-size: 0.875rem;
      color: var(--muted);
      text-decoration: none;
      margin-bottom: 40px;
    }

    .back-link:hover { color: var(--blue); }

    h1 {
      font-size: clamp(1.5rem, 3vw, 2rem);
      font-weight: 600;
      color: var(--text);
      line-height: 1.2;
      letter-spacing: -0.02em;
    }

    .client-label {
      font-size: 1rem;
      color: var(--muted);
      margin-top: 4px;
      margin-bottom: 48px;
    }

    .section-label {
      font-size: 0.7rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--blue);
      margin-bottom: 14px;
    }

    .section-block {
      margin-top: 40px;
    }

    p {
      font-size: 1rem;
      line-height: 1.5;
      color: #333;
      margin-bottom: 12px;
    }

    p:last-child { margin-bottom: 0; }

    .outcome-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .outcome-list li {
      font-size: 0.9375rem;
      line-height: 1.5;
      color: #333;
      padding-left: 16px;
      position: relative;
    }

    .outcome-list li::before {
      content: '';
      position: absolute;
      left: 0;
      top: 9px;
      width: 5px;
      height: 5px;
      border-radius: 50%;
      background: var(--blue);
    }

    .bottom-cta {
      margin-top: 56px;
      padding-top: 32px;
      border-top: 1px solid var(--border);
      font-size: 1rem;
      color: var(--muted);
      line-height: 1.5;
    }

    .bottom-cta a {
      color: var(--blue);
      text-decoration: none;
    }

    .bottom-cta a:hover { text-decoration: underline; }

    @media (max-width: 860px) {
      :root { --pad: 24px; }
      nav { padding: 0 24px; }
      .nav-links { gap: 20px; }
    }
  </style>
</head>
<body>
  <nav>
    <a href="index.html" class="logo">studio cartelli</a>
    <ul class="nav-links">
      <li><a href="projects.html" class="active">Projects</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
    </ul>
  </nav>

  <div class="content">
    <a href="projects.html" class="back-link">← Back to Projects</a>

    <h1>Precision Alert Monitoring</h1>
    <p class="client-label">Dataminr</p>

    <div class="section-block">
      <div class="section-label">Problem</div>
      <p>100,000+ security analysts were spending 3–4 hours every week manually reconfiguring alert coverage. The platform used fixed radius settings — every alert type shared the same geographic boundary, so analysts received noise from irrelevant areas and missed threats near assets that mattered. The workarounds were everywhere: duplicate alerts, quarterly manual resets, support tickets for configurations the product should have handled.</p>
      <p>An acquisition-driven pivot threatened to make it worse. Stakeholders wanted to change product direction without evidence.</p>
    </div>

    <div class="section-block">
      <div class="section-label">Insight</div>
      <p>Users don't think in radius circles. They think in proximity to assets. The moment the frame shifted from geometric coverage to contextual coverage, the right product direction became clear. Research evidence stopped the acquisition pivot and redirected 18–24 months of potential development waste.</p>
    </div>

    <div class="section-block">
      <div class="section-label">Outcome</div>
      <ul class="outcome-list">
        <li>20% reduction in alert noise</li>
        <li>65% reduction in configuration time — from 3–4 hours to 1–1.5 hours weekly</li>
        <li>50% fewer duplicate workarounds</li>
        <li>90% elimination of quarterly manual resets</li>
        <li>45% drop in support tickets, 40% increase in adoption</li>
        <li>RFP differentiator for 10,000+ accounts</li>
      </ul>
    </div>

    <p class="bottom-cta">Working on something similar? <a href="mailto:ciao@studiocartelli.com">Get in touch.</a></p>
  </div>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

- [ ] "← Back to Projects" link renders in muted gray, navigates to projects.html
- [ ] h1 title and client label render correctly
- [ ] Three labeled sections: PROBLEM, INSIGHT, OUTCOME in blue uppercase
- [ ] OUTCOME renders as a bullet list with blue dots
- [ ] Bottom CTA "Get in touch." is a blue inline link
- [ ] Content is max 720px centered, comfortable line length
- [ ] Resize below 860px: 24px gutters, readable

- [ ] **Step 3: Commit**

```bash
cd /Users/pcartelli/patcartelli.github.io
git add precision-alert-monitoring.html
git commit -m "feat: add Precision Alert Monitoring case study"
```

---

## Task 5: Case study — Mission-Critical Trust

**Files:**
- Create: `mission-critical-trust.html`

- [ ] **Step 1: Create mission-critical-trust.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Mission-Critical Trust — Studio Cartelli case study. Dashboard customization for 250,000+ analysts, 40% adoption increase.">
  <title>Mission-Critical Trust — Studio Cartelli</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Syne+Tactile&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --blue: #005BEC;
      --text: #1a1a1a;
      --muted: #555;
      --light: #999;
      --border: #e8e8e8;
      --pad: 80px;
      --nav-h: 72px;
    }

    html, body { min-height: 100%; }

    body {
      background: white;
      font-family: 'Inter', sans-serif;
      color: var(--text);
    }

    nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: white;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: var(--nav-h);
      padding: 0 var(--pad);
    }

    .logo {
      font-family: 'Syne Tactile', sans-serif;
      font-size: 1.25rem;
      color: var(--blue);
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 32px;
      list-style: none;
    }

    .nav-links a {
      font-size: 0.875rem;
      font-weight: 500;
      color: var(--muted);
      text-decoration: none;
    }

    .nav-links a.active { color: var(--text); }

    .content {
      max-width: 720px;
      margin: 0 auto;
      padding: var(--pad);
    }

    .back-link {
      display: inline-block;
      font-size: 0.875rem;
      color: var(--muted);
      text-decoration: none;
      margin-bottom: 40px;
    }

    .back-link:hover { color: var(--blue); }

    h1 {
      font-size: clamp(1.5rem, 3vw, 2rem);
      font-weight: 600;
      color: var(--text);
      line-height: 1.2;
      letter-spacing: -0.02em;
    }

    .client-label {
      font-size: 1rem;
      color: var(--muted);
      margin-top: 4px;
      margin-bottom: 48px;
    }

    .section-label {
      font-size: 0.7rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--blue);
      margin-bottom: 14px;
    }

    .section-block { margin-top: 40px; }

    p {
      font-size: 1rem;
      line-height: 1.5;
      color: #333;
      margin-bottom: 12px;
    }

    p:last-child { margin-bottom: 0; }

    .outcome-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .outcome-list li {
      font-size: 0.9375rem;
      line-height: 1.5;
      color: #333;
      padding-left: 16px;
      position: relative;
    }

    .outcome-list li::before {
      content: '';
      position: absolute;
      left: 0;
      top: 9px;
      width: 5px;
      height: 5px;
      border-radius: 50%;
      background: var(--blue);
    }

    .bottom-cta {
      margin-top: 56px;
      padding-top: 32px;
      border-top: 1px solid var(--border);
      font-size: 1rem;
      color: var(--muted);
      line-height: 1.5;
    }

    .bottom-cta a {
      color: var(--blue);
      text-decoration: none;
    }

    .bottom-cta a:hover { text-decoration: underline; }

    @media (max-width: 860px) {
      :root { --pad: 24px; }
      nav { padding: 0 24px; }
      .nav-links { gap: 20px; }
    }
  </style>
</head>
<body>
  <nav>
    <a href="index.html" class="logo">studio cartelli</a>
    <ul class="nav-links">
      <li><a href="projects.html" class="active">Projects</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
    </ul>
  </nav>

  <div class="content">
    <a href="projects.html" class="back-link">← Back to Projects</a>

    <h1>Mission-Critical Trust</h1>
    <p class="client-label">Dataminr</p>

    <div class="section-block">
      <div class="section-label">Problem</div>
      <p>Security managers at 250,000+ analyst accounts couldn't trust what Dataminr delivered. There was no way to preview changes before they went live, no visibility into what configurations were active, and no way to verify that content hadn't drifted. Errors reached analysts in the field — the people making high-stakes decisions in real time.</p>
      <p>Public sector stakeholders resisted user research, making it difficult to surface the real problem. The roadmap was being planned around dashboard management features that weren't what users needed.</p>
    </div>

    <div class="section-block">
      <div class="section-label">Insight</div>
      <p>Dashboard management wasn't the priority. The real pain was trusted content assignment at scale: the ability to know that the right information was reaching the right analysts, consistently and verifiably. Discovery sessions with resistant stakeholders shifted the entire roadmap once the evidence was in front of them.</p>
    </div>

    <div class="section-block">
      <div class="section-label">Outcome</div>
      <ul class="outcome-list">
        <li>Dashboard customization shipped for 250,000+ analysts</li>
        <li>45% drop in support tickets, 40% increase in adoption</li>
        <li>Unblocked expansion into 10,000+ user accounts</li>
        <li>Reusable bulk action patterns deployed across 3 other admin interfaces</li>
        <li>Progressive disclosure pattern became Dataminr's standard for high-risk operations</li>
      </ul>
    </div>

    <p class="bottom-cta">Working on something similar? <a href="mailto:ciao@studiocartelli.com">Get in touch.</a></p>
  </div>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

- [ ] "← Back to Projects" navigates to projects.html
- [ ] Three sections render correctly with PROBLEM / INSIGHT / OUTCOME labels
- [ ] Outcome list has blue bullet dots
- [ ] Bottom CTA present
- [ ] Layout matches precision-alert-monitoring.html visually

- [ ] **Step 3: Commit**

```bash
cd /Users/pcartelli/patcartelli.github.io
git add mission-critical-trust.html
git commit -m "feat: add Mission-Critical Trust case study"
```

---

## Task 6: Case study — Strategic Reporting at Scale

**Files:**
- Create: `strategic-reporting.html`

- [ ] **Step 1: Create strategic-reporting.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Strategic Reporting at Scale — Studio Cartelli case study. Daily exports eliminated, 100% beta acceptance at Vividly.">
  <title>Strategic Reporting at Scale — Studio Cartelli</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Syne+Tactile&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --blue: #005BEC;
      --text: #1a1a1a;
      --muted: #555;
      --light: #999;
      --border: #e8e8e8;
      --pad: 80px;
      --nav-h: 72px;
    }

    html, body { min-height: 100%; }

    body {
      background: white;
      font-family: 'Inter', sans-serif;
      color: var(--text);
    }

    nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: white;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: var(--nav-h);
      padding: 0 var(--pad);
    }

    .logo {
      font-family: 'Syne Tactile', sans-serif;
      font-size: 1.25rem;
      color: var(--blue);
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 32px;
      list-style: none;
    }

    .nav-links a {
      font-size: 0.875rem;
      font-weight: 500;
      color: var(--muted);
      text-decoration: none;
    }

    .nav-links a.active { color: var(--text); }

    .content {
      max-width: 720px;
      margin: 0 auto;
      padding: var(--pad);
    }

    .back-link {
      display: inline-block;
      font-size: 0.875rem;
      color: var(--muted);
      text-decoration: none;
      margin-bottom: 40px;
    }

    .back-link:hover { color: var(--blue); }

    h1 {
      font-size: clamp(1.5rem, 3vw, 2rem);
      font-weight: 600;
      color: var(--text);
      line-height: 1.2;
      letter-spacing: -0.02em;
    }

    .client-label {
      font-size: 1rem;
      color: var(--muted);
      margin-top: 4px;
      margin-bottom: 48px;
    }

    .section-label {
      font-size: 0.7rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--blue);
      margin-bottom: 14px;
    }

    .section-block { margin-top: 40px; }

    p {
      font-size: 1rem;
      line-height: 1.5;
      color: #333;
      margin-bottom: 12px;
    }

    p:last-child { margin-bottom: 0; }

    .outcome-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .outcome-list li {
      font-size: 0.9375rem;
      line-height: 1.5;
      color: #333;
      padding-left: 16px;
      position: relative;
    }

    .outcome-list li::before {
      content: '';
      position: absolute;
      left: 0;
      top: 9px;
      width: 5px;
      height: 5px;
      border-radius: 50%;
      background: var(--blue);
    }

    .bottom-cta {
      margin-top: 56px;
      padding-top: 32px;
      border-top: 1px solid var(--border);
      font-size: 1rem;
      color: var(--muted);
      line-height: 1.5;
    }

    .bottom-cta a {
      color: var(--blue);
      text-decoration: none;
    }

    .bottom-cta a:hover { text-decoration: underline; }

    @media (max-width: 860px) {
      :root { --pad: 24px; }
      nav { padding: 0 24px; }
      .nav-links { gap: 20px; }
    }
  </style>
</head>
<body>
  <nav>
    <a href="index.html" class="logo">studio cartelli</a>
    <ul class="nav-links">
      <li><a href="projects.html" class="active">Projects</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
    </ul>
  </nav>

  <div class="content">
    <a href="projects.html" class="back-link">← Back to Projects</a>

    <h1>Strategic Reporting at Scale</h1>
    <p class="client-label">Vividly</p>

    <div class="section-block">
      <div class="section-label">Problem</div>
      <p>CPG finance teams were exporting data from the platform 3–5 times a day. The platform couldn't support the analysis they needed to do their jobs, so they did it in spreadsheets instead. This was a churn risk across mid-market accounts and a competitive vulnerability.</p>
      <p>The internal assumption was that users wanted mindmap-style visualizations — a direction based on what competitors were building, not on what users actually needed.</p>
    </div>

    <div class="section-block">
      <div class="section-label">Insight</div>
      <p>Users needed content management that matched how they already organized their business. CPG companies run on ERP hierarchies: folders within folders, matching their product and customer structure. Prototyping with real CPG data — not competitor patterns — made this legible to stakeholders who had been resistant to departing from the market.</p>
    </div>

    <div class="section-block">
      <div class="section-label">Outcome</div>
      <ul class="outcome-list">
        <li>Daily exports dropped from 3–5 per day to as-needed</li>
        <li>100% of beta users accepted manual setup of the new hierarchy structure</li>
        <li>Validated at scale: 500 products and 800+ customers under 2-second performance</li>
        <li>Reduced churn threat across mid-market accounts</li>
        <li>Improvements unlocked new workflows across Budget, Forecast, and demand planning</li>
      </ul>
    </div>

    <p class="bottom-cta">Working on something similar? <a href="mailto:ciao@studiocartelli.com">Get in touch.</a></p>
  </div>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

- [ ] Three sections render with correct labels and content
- [ ] Outcome list renders with blue dots
- [ ] Layout matches previous case study pages
- [ ] "← Back to Projects" navigates correctly

- [ ] **Step 3: Commit**

```bash
cd /Users/pcartelli/patcartelli.github.io
git add strategic-reporting.html
git commit -m "feat: add Strategic Reporting at Scale case study"
```

---

## Task 7: Case study — The Check-In Problem

**Files:**
- Create: `check-in-problem.html`

- [ ] **Step 1: Create check-in-problem.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="The Check-In Problem — Studio Cartelli case study. First baseline metrics across 2.3M check-ins, phased strategy for Gympass.">
  <title>The Check-In Problem — Studio Cartelli</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Syne+Tactile&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }

    :root {
      --blue: #005BEC;
      --text: #1a1a1a;
      --muted: #555;
      --light: #999;
      --border: #e8e8e8;
      --pad: 80px;
      --nav-h: 72px;
    }

    html, body { min-height: 100%; }

    body {
      background: white;
      font-family: 'Inter', sans-serif;
      color: var(--text);
    }

    nav {
      position: sticky;
      top: 0;
      z-index: 100;
      background: white;
      border-bottom: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: var(--nav-h);
      padding: 0 var(--pad);
    }

    .logo {
      font-family: 'Syne Tactile', sans-serif;
      font-size: 1.25rem;
      color: var(--blue);
      text-decoration: none;
    }

    .nav-links {
      display: flex;
      gap: 32px;
      list-style: none;
    }

    .nav-links a {
      font-size: 0.875rem;
      font-weight: 500;
      color: var(--muted);
      text-decoration: none;
    }

    .nav-links a.active { color: var(--text); }

    .content {
      max-width: 720px;
      margin: 0 auto;
      padding: var(--pad);
    }

    .back-link {
      display: inline-block;
      font-size: 0.875rem;
      color: var(--muted);
      text-decoration: none;
      margin-bottom: 40px;
    }

    .back-link:hover { color: var(--blue); }

    h1 {
      font-size: clamp(1.5rem, 3vw, 2rem);
      font-weight: 600;
      color: var(--text);
      line-height: 1.2;
      letter-spacing: -0.02em;
    }

    .client-label {
      font-size: 1rem;
      color: var(--muted);
      margin-top: 4px;
      margin-bottom: 48px;
    }

    .section-label {
      font-size: 0.7rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.1em;
      color: var(--blue);
      margin-bottom: 14px;
    }

    .section-block { margin-top: 40px; }

    p {
      font-size: 1rem;
      line-height: 1.5;
      color: #333;
      margin-bottom: 12px;
    }

    p:last-child { margin-bottom: 0; }

    .outcome-list {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }

    .outcome-list li {
      font-size: 0.9375rem;
      line-height: 1.5;
      color: #333;
      padding-left: 16px;
      position: relative;
    }

    .outcome-list li::before {
      content: '';
      position: absolute;
      left: 0;
      top: 9px;
      width: 5px;
      height: 5px;
      border-radius: 50%;
      background: var(--blue);
    }

    .bottom-cta {
      margin-top: 56px;
      padding-top: 32px;
      border-top: 1px solid var(--border);
      font-size: 1rem;
      color: var(--muted);
      line-height: 1.5;
    }

    .bottom-cta a {
      color: var(--blue);
      text-decoration: none;
    }

    .bottom-cta a:hover { text-decoration: underline; }

    @media (max-width: 860px) {
      :root { --pad: 24px; }
      nav { padding: 0 24px; }
      .nav-links { gap: 20px; }
    }
  </style>
</head>
<body>
  <nav>
    <a href="index.html" class="logo">studio cartelli</a>
    <ul class="nav-links">
      <li><a href="projects.html" class="active">Projects</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html">About</a></li>
    </ul>
  </nav>

  <div class="content">
    <a href="projects.html" class="back-link">← Back to Projects</a>

    <h1>The Check-In Problem</h1>
    <p class="client-label">Gympass</p>

    <div class="section-block">
      <div class="section-label">Problem</div>
      <p>Users weren't checking in at partner gyms, costing Gympass nearly six figures annually in manual verification across 2.3 million check-ins. The internal assumption was user forgetfulness, which pointed toward reminder features and notification nudges.</p>
      <p>Direct user research wasn't available across 16 countries. The team needed a way to understand the problem without it.</p>
    </div>

    <div class="section-block">
      <div class="section-label">Insight</div>
      <p>Gympass was the only platform requiring dual validation at check-in. No competitor did this. The friction wasn't a user behavior problem — it was a system design problem the platform had created and then blamed on its users. Service blueprints, quantitative analysis, and behavioral data made this visible without needing direct access to users across every market.</p>
    </div>

    <div class="section-block">
      <div class="section-label">Outcome</div>
      <ul class="outcome-list">
        <li>First comprehensive baseline metrics established across check-in rates by business type, country, and user segment</li>
        <li>Phased strategy (immediate, medium, and long-term) addressed root causes rather than symptoms</li>
        <li>Framework guided the team's reopening roadmap after COVID</li>
        <li>Cross-functional alignment maintained around ecosystem thinking rather than isolated feature fixes</li>
      </ul>
    </div>

    <p class="bottom-cta">Working on something similar? <a href="mailto:ciao@studiocartelli.com">Get in touch.</a></p>
  </div>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

- [ ] Three sections render with correct labels and content
- [ ] Outcome list renders with blue dots
- [ ] "← Back to Projects" navigates to projects.html
- [ ] Layout matches previous case study pages

- [ ] **Step 3: Commit**

```bash
cd /Users/pcartelli/patcartelli.github.io
git add check-in-problem.html
git commit -m "feat: add The Check-In Problem case study"
```

---

## Task 8: Update `about.html`

**Files:**
- Modify: `about.html`

Three changes: nav labels (Work → Projects, add Services), line-height 1.7 → 1.5, add `.content` max-width wrapper.

- [ ] **Step 1: Update nav links in about.html**

Find this block in `about.html`:

```html
    <ul class="nav-links">
      <li><a href="index.html">Home</a></li>
      <li><a href="work.html">Work</a></li>
      <li><a href="about.html" class="active" aria-current="page">About</a></li>
    </ul>
```

Replace with:

```html
    <ul class="nav-links">
      <li><a href="projects.html">Projects</a></li>
      <li><a href="services.html">Services</a></li>
      <li><a href="about.html" class="active" aria-current="page">About</a></li>
    </ul>
```

- [ ] **Step 2: Update line-height in about.html**

Find in `about.html` CSS:

```css
  p {
    font-size: 1rem;
    line-height: 1.7;
    color: #333;
    margin-bottom: 16px;
  }
```

Replace with:

```css
  p {
    font-size: 1rem;
    line-height: 1.5;
    color: #333;
    margin-bottom: 16px;
  }
```

- [ ] **Step 3: Add .content max-width wrapper**

In `about.html` CSS, find the `.page` rule:

```css
  .page { padding: var(--pad); }
```

Replace with:

```css
  .page { padding: var(--pad); }

  .content {
    max-width: 720px;
    margin: 0 auto;
  }
```

`.page` keeps the padding. `.content` only constrains the max-width — no padding on `.content` here, unlike the other pages where `.content` carries both.

Then in the HTML, wrap the contents of `<div class="page">` in `<div class="content">`:

Find:
```html
  <div class="page">

    <div class="hero">
```

Replace with:
```html
  <div class="page">
    <div class="content">

    <div class="hero">
```

Find the closing `</div>` of `.page` (last `</div>` before `</body>`):

```html
  </div>


</body>
```

Replace with:
```html
    </div>
  </div>


</body>
```

- [ ] **Step 4: Open in browser and verify**

- [ ] Nav shows Projects / Services / About (no Home, no Work)
- [ ] About link is active (dark)
- [ ] Content area is noticeably narrower on wide screens, centered
- [ ] Body text line-height feels tighter than before (1.5 vs 1.7)
- [ ] Two-col layout still intact, experience list renders correctly

- [ ] **Step 5: Commit**

```bash
cd /Users/pcartelli/patcartelli.github.io
git add about.html
git commit -m "fix: update about.html nav, line-height, and content max-width"
```

---

## Task 9: Cross-page smoke test + final commit

- [ ] **Step 1: Verify full navigation flow in browser**

Open `index.html` and walk through every link:

- [ ] Home → Projects: "View Projects" CTA navigates to projects.html
- [ ] Home → Get in Touch: opens mail client with ciao@studiocartelli.com
- [ ] Projects → each case study: all four cards navigate correctly
- [ ] Each case study → Back to Projects: returns to projects.html
- [ ] Nav logo on every page: returns to index.html
- [ ] Nav "About" on every page: navigates to about.html
- [ ] Nav "Projects" on every page: navigates to projects.html
- [ ] Nav "Services" on every page: navigates to a 404 (expected — not yet built)

- [ ] **Step 2: Verify active nav state on each page**

- [ ] `index.html`: no nav link is active
- [ ] `projects.html`: Projects link is dark
- [ ] All case study pages: Projects link is dark (active, since they're sub-pages of Projects)
- [ ] `about.html`: About link is dark

- [ ] **Step 3: Verify responsive at 860px**

Resize browser to 860px on each page:

- [ ] `index.html`: blue panel stacks — hero text first, availability/services row below
- [ ] `projects.html`: 24px gutters, cards full width, readable
- [ ] Case study pages: 24px gutters, text readable at full width
- [ ] `about.html`: two-col collapses to single column

- [ ] **Step 4: Push to GitHub Pages**

```bash
cd /Users/pcartelli/patcartelli.github.io
git push origin main
```

Expected: GitHub Pages builds and deploys automatically. Site live at studiocartelli.com within ~60 seconds.

- [ ] **Step 5: Verify live site**

Open https://studiocartelli.com and repeat the navigation smoke test from Step 1.
