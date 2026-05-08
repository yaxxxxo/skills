---
name: interactive-html-explainer
description: Use when the user asks to explain a topic as an interactive HTML page, visual explainer, or rich guide — triggered by "make me an interactive page about X", "create a visual explainer for X", "explain X as HTML", or any explicit request for an HTML learning artifact. Do NOT trigger on general "explain X" or "teach me X" requests without an HTML/visual qualifier.
---

# Interactive HTML Explainer

## Overview

Produce a self-contained, single-file HTML explainer that teaches a topic through interactive navigation, animated elements, and research-backed content. No CDN links, no external dependencies — everything inline. Apply maximum reasoning effort throughout the entire workflow.

## Workflow (in order)

**1. Web search** — Run 3–5 targeted searches to gather authoritative data before writing anything. Look for: key statistics, common misconceptions, primary sources (official organisations, government sites, institutional research, established journalism). Never invent a number — every specific statistic must come from a real, web-searched URL.

**2. Plan sections** — Decide which sections fit this topic (see below). For each section, identify the inverted-pyramid lead: the single most important insight a reader should leave with.

**3. Write the HTML** — With research complete and section plan set, write the full file in one pass.

## Sections

**Always required (3):**
| Section | Purpose |
|---------|---------|
| Overview | What it is, why it matters, 3–5 key stats with sources |
| How It Works | The core mechanics, rules, or process |
| One contextual deep-dive | Choose based on topic (History, Structure, Key Players, etc.) |

**Optional — include if they add genuine value (up to 3 more):**
Economics / Scale · Culture & Impact · Controversies · Key People · Timeline · Comparisons

## Interactive Elements — Pick by Topic Shape

Sticky tab bar and hover tooltips on jargon are **always included**. For the rest, match element to topic:

| If the topic has… | Use… |
|---|---|
| A sequence of events | Click-to-expand timeline |
| Parallel comparable items (roles, types, countries) | Card grid |
| A process or lifecycle | Phase/step flow |
| Rules, FAQs, or dense "things to know" | Collapsible accordion |
| Key stats | Animated stat counters (trigger on scroll) |

Pick **2–3 beyond the tab bar**. Don't use all of them — overcrowding reduces clarity.

## Cognitive Learning Rules

**Hard rules (non-negotiable):**
- **Inverted pyramid:** The most important insight goes in the first sentence of every section — not buried at the end
- **Concrete before abstract:** Show a real example before explaining the concept. Never lead with theory
- **Prior knowledge bridge:** The hero section opens with an analogy to something the reader almost certainly already understands

**Guidelines:**
- Chunking: max ~3 ideas per visual unit (card, accordion item, timeline entry)
- Dual coding: major concepts get both a text explanation and a visual representation
- Signaling: bold exactly one key phrase per paragraph — not multiple

## Sources

- **Hover tooltips on specific stats and claims** — reader never loses their place
- **Dedicated "Sources" tab** — full list of URLs for readers who want to go deeper
- Source priority: official/primary sources → institutional/academic → established journalism (Reuters, FT, BBC, Economist) → Wikipedia as structure only, never as terminal citation

## Design System

```css
:root {
  --primary: #17408B;   /* adjust to topic's visual identity */
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

Dark background always. Tie `--primary`/`--accent` to the topic's brand colors (team colors, flag colors, company palette, etc.).

## HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head><!-- meta, title, <style> --></head>
<body>
  <header class="hero">       <!-- gradient, title, prior-knowledge analogy, badge -->
  <nav class="tab-bar">       <!-- sticky tab buttons -->
  <section class="section active" id="tab-overview">
  <section class="section" id="tab-how-it-works">
  <section class="section" id="tab-[deep-dive]">
  <!-- optional sections -->
  <section class="section" id="tab-sources">
  <footer>
  <script>                    <!-- tab switching + element logic -->
</body>
</html>
```

**Tab switching (always use this exact pattern — forgetting to deactivate all tabs is the most common bug):**
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

## Output

Save as `<topic-slug>.html` in the current working directory (e.g. `nba.html`, `eu-carbon-market.html`).

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Using Bootstrap/Tailwind CDN | All CSS inline — no network requests |
| Leading with definition, not insight | Inverted pyramid: most important thing first |
| Abstract explanation before example | Concrete first, always |
| Inventing statistics | Web search every number before using it |
| Too many interactive widgets | 2–3 beyond the tab bar max |
| Generic dark colors | Tie colors to the topic's visual identity |
| Forgetting mobile | Use `clamp()` for font sizes; `flex-wrap` for grids |

## Pre-Handover Checklist

- [ ] Every statistic has a real source URL (hover tooltip + Sources tab)
- [ ] Each section opens with its most important insight (inverted pyramid)
- [ ] Hero contains a prior-knowledge analogy
- [ ] At least one concrete example precedes each abstract concept
- [ ] Interactive elements match topic shape (not copied from NBA example)
- [ ] Tab switching uses the exact pattern above
- [ ] No external URLs in `<link>` or `<script src>` tags
