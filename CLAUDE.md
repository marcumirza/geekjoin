# GeekJoin — Project Handoff for Claude Code

## Project Overview
GeekJoin is a presentation/landing page website for a collaborative platform where students build real projects and get discovered by companies. The site was designed to serve as a demo/waitlist page before the actual app is built.

## Files
- `index.html` — Main dark Apple-style website (current version)
- `index-original-light.html` — Original light/clean version (backup)
- `CLAUDE.md` — This file

## Current State
The site is a **single-file static HTML** page. Everything (HTML, CSS, JS) lives in `index.html`. No build tools, no dependencies, no npm — just open in a browser.

---

## Sections (in order)
1. **Nav** — Fixed top bar with links + "Join Waitlist" CTA
2. **Hero** — Headline, subtext, two CTAs, 3-photo grid from Unsplash
3. **Stats** — 4-column stat bar
4. **Problem** — 3 problem cards with red top accent
5. **Solution** — Split layout: photo with live project badge + checklist
6. **Features (Bento grid)** — 6 cards in Apple bento style, 2 with photos
7. **Photo Story** — 7-cell mosaic grid of student collaboration photos
8. **How It Works** — 4-step horizontal grid
9. **Who It's For** — Side-by-side cards: Students vs Companies
10. **What Makes Us Different** — 4 dark cards on dark bg
11. **Journey Map** — Interactive genealogical tree (click-to-expand detail boxes)
12. **Waitlist** — Embedded Tally.so form (form ID: rj2D5l)
13. **Footer**

---

## Journey Map — Key Logic
The journey map section (`#journey`) is the most complex interactive piece.

### How it works
- Each step is a `.jnode` div with:
  - `data-tip` — tooltip title (shown in the popup)
  - `data-body` — tooltip description text
  - `data-side` — which side the popup appears (`"left"` or `"right"`)
- **Click** a node → popup appears on the assigned side, right beside the card
- **Click same node again** → closes it
- **Click anywhere else** or press **Escape** → closes
- **✕ button** in popup corner also closes it
- Popup animates in with fade + scale

### Left/Right pattern (top to bottom)
| Step | Side |
|---|---|
| Project idea | left |
| Post the project | right |
| Have an idea | left |
| Have skills | right |
| Right team formed | left |
| Build & document | right |
| Timeline | left |
| Agile / Scrum | right |
| Skill endorsements | left |
| Companies observe | right |
| Company reaches out | left |
| Interview | right |
| Internship | left |
| Job offer | right |

### Popup positioning logic (JS)
```js
// Uses getBoundingClientRect() + position: fixed
// data-side="left"  → popup appears to the LEFT of the card (rect.left - tw - gap)
// data-side="right" → popup appears to the RIGHT of the card (rect.right + gap)
// Safety fallback: flips side if popup would go off-screen
// Vertically: centers on the card (rect.top + height/2 - 55), clamped to viewport
```

---

## Tally Waitlist Form
- Form share URL: `https://tally.so/r/rj2D5l`
- Embed ID used: `rj2D5l`
- Embedded via iframe with Tally's embed.js script
- Located in `#waitlist` section

---

## Design System
All CSS is inline in `<style>` blocks within `index.html`.

### CSS Variables (root)
```css
--bg: #000000          /* page background */
--bg-2: #0a0a0a        /* alternate section bg */
--bg-3: #111111        /* card backgrounds */
--bg-4: #1a1a1a        /* hover state */
--border: rgba(255,255,255,0.08)
--border-bright: rgba(255,255,255,0.15)
--text: #f5f5f7
--text-2: #a1a1a6
--text-3: #6e6e73
--blue: #2997ff        /* primary accent */
--green: #30d158       /* success/students */
--purple: #bf5af2      /* secondary accent */
--orange: #ff9f0a      /* warning/highlight */
--radius: 18px
```

### Font
Inter (Google Fonts) with system-ui fallback.

### Photos
All photos are Unsplash free-to-use URLs (no API key needed):
- Hero: `photo-1522202176988`, `photo-1531482615713`, `photo-1515187029135`
- Solution: `photo-1600880292203`
- Features bento: `photo-1556761175`, `photo-1519389950473`
- Story grid: `photo-1543269664`, `photo-1529156069898`, `photo-1573496359142`, `photo-1507537297725`, `photo-1582213782179`, `photo-1498050108023`

---

## Possible Next Steps (what to build in Claude Code)
- [ ] Convert to a proper React/Next.js app
- [ ] Replace Unsplash URLs with locally hosted or CDN images
- [ ] Add real backend for waitlist (replace Tally with custom API)
- [ ] Build the actual GeekJoin app (auth, projects, teams, company dashboard)
- [ ] Add SEO meta tags, OG image, favicon
- [ ] Deploy to Vercel/Netlify with custom domain (e.g. geekjoin.io)
- [ ] Replace placeholder stats with real numbers once users sign up
- [ ] Add analytics (Plausible, Posthog, or Google Analytics)

---

## Conversation Summary
This project was built in Cowork mode (Claude desktop app). The full conversation covered:
1. Reading the original TeamUp MVP doc (uploaded .docx)
2. Building a clean light HTML landing page
3. Redesigning to dark Apple-style with real photos
4. Renaming from TeamUp → GeekJoin
5. Adding an interactive journey map (genealogical tree)
6. Adding click-triggered detail popups on the journey map nodes
7. Embedding a real Tally.so waitlist form

The original light version is preserved in `index-original-light.html`.
