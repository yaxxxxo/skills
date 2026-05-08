---
name: interactive-html-explainer
description: Use when the user asks to explain a topic, concept, or system as a rich visual document — triggered by "explain X", "create a guide for X", "teach me about X", "make an explainer for X", or any request to turn a topic into an interactive HTML page.
---

# Interactive HTML Explainer

## Overview

Produce a self-contained, single-file HTML explainer that teaches a topic through interactive navigation, animated elements, and layered depth. No CDN links, no external dependencies — everything inline.

## When to Use

- "Explain X to me" / "create a guide to X"
- User wants to understand something from scratch
- Topic has enough structure to benefit from sections (history, how it works, key rules, economics, culture)

**Don't use when:** user wants a quick text answer — this is a ~300-line HTML artifact.

## Core Pattern

### 1. Always Include These Sections (adapt names to topic)

| Section | Purpose |
|---------|---------|
| Overview | What is it, why it matters, key stats |
| History / Origin | Timeline of how it came to be |
| Structure / Components | How it's organized (teams, parts, layers, etc.) |
| How It Works | The mechanics / rules / process |
| Economics / Business | Money, incentives, scale |
| Culture / Impact | Broader significance |

Not every topic needs all six — cut ones that don't add value.

### 2. Always Include These Interactive Elements

| Element | When |
|---------|------|
| Sticky tab bar | Always — main navigation between sections |
| Animated stat counters | Overview section — 3-5 key numbers that count up on scroll |
| Collapsible accordion | Rules, FAQs, or any list of "things to know" |
| Click-to-expand timeline | History section |
| Hover tooltips (`data-tip`) | Inline on jargon words |
| Card grid | For parallel concepts (positions, roles, types) |
| Phase/step flow | For sequential processes (season, pipeline, lifecycle) |

Pick 2-3 beyond the tab bar and timeline. Don't use all of them — overcrowding reduces clarity.

### 3. Design System (copy verbatim, then customize colors)

```css
:root {
  --primary: #17408B;   /* adjust to topic */
  --accent:  #C9082A;   /* adjust to topic */
  --highlight: #f5a623;
  --bg: #0d0d0d;
  --surface: #1a1a2e;
  --surface2: #16213e;
  --text: #e8e8f0;
  --text-dim: #9999bb;
  --radius: 12px;
  --transition: 0.3s ease;
}
```

Dark background always. Use `--primary` / `--accent` as the topic's brand colors (sport team colors, company palette, flag colors, etc.).

### 4. File Output

- Single `.html` file, no external assets
- All CSS in `<style>` block in `<head>`
- All JS in `<script>` block before `</body>`
- Open in browser with `cmd.exe /c start "" "$(wslpath -w /path/to/file.html)"` on WSL

## HTML Structure Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- meta, title, <style> with full CSS -->
</head>
<body>
  <header class="hero">          <!-- gradient hero, title, subtitle, badge -->
  <nav class="tab-bar">          <!-- sticky tab buttons -->
  <section class="section active" id="tab-overview">
  <section class="section" id="tab-history">
  <section class="section" id="tab-structure">
  <section class="section" id="tab-howit works">
  <section class="section" id="tab-economics">
  <section class="section" id="tab-culture">
  <footer>
  <script>                       <!-- tab switching + interactive element logic -->
</body>
</html>
```

## Key Reusable JS Patterns

**Tab switching (always include):**
```js
document.querySelectorAll('.tab-btn').forEach(btn => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.tab-btn, .section')
      .forEach(el => el.classList.remove('active'));
    btn.classList.add('active');
    document.getElementById('tab-' + btn.dataset.tab).classList.add('active');
  });
});
```

**Animated counter (for stat chips):**
```js
function animateCount(el, target) {
  let n = 0; const step = Math.ceil(target / 40);
  const t = setInterval(() => {
    n = Math.min(n + step, target);
    el.textContent = n;
    if (n >= target) clearInterval(t);
  }, 30);
}
// Trigger on IntersectionObserver when stat row enters viewport
```

**Accordion:**
```js
document.querySelectorAll('.acc-header').forEach(h => {
  h.addEventListener('click', () => {
    const open = h.classList.contains('open');
    document.querySelectorAll('.acc-header').forEach(x => {
      x.classList.remove('open');
      x.nextElementSibling.classList.remove('open');
    });
    if (!open) { h.classList.add('open'); h.nextElementSibling.classList.add('open'); }
  });
});
```

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Using Bootstrap/Tailwind CDN | All CSS must be inline — no network requests |
| Too many interactive widgets | Pick 3-4 max; clarity beats novelty |
| Forgetting mobile | Use `clamp()` for font sizes; flex-wrap for grids |
| Generic dark colors | Tie `--primary`/`--accent` to the topic's visual identity |
| Forgetting to open the file | After writing, run the `cmd.exe /c start` or `wslview` command |

## Checklist Before Handing Over

- [ ] All 6 sections present (or consciously cut ones that don't fit)
- [ ] Stat counters animate on scroll into view
- [ ] At least one accordion and one timeline
- [ ] Hover tooltips on ≥3 jargon terms
- [ ] No external URLs in `<link>` or `<script src>` tags
- [ ] File opens without errors in browser
