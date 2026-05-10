---
name: interactive-html-explainer
description: Produces a self-contained interactive HTML explainer with tabbed navigation, animated stats, and sourced citations. Use when user asks to explain a topic as an interactive HTML page or visual explainer — triggered by "make me an interactive page about X", "create a visual explainer for X", "explain X as HTML". Do NOT trigger on plain "explain X" without an HTML/visual qualifier.
---

# Interactive HTML Explainer

## Quick start

1. **Web search** — 3–5 targeted searches for key stats and authoritative sources. Never invent a number.
2. **Plan sections** — pick 3 required + up to 3 optional (see [REFERENCE.md](REFERENCE.md))
3. **Write** — single `.html` file, no external dependencies. Save as `<topic-slug>.html` in cwd.

Apply maximum reasoning effort throughout.

## Workflows

### Sections

**Always required (3):**
- Overview — what it is, why it matters, 3–5 sourced stats
- How It Works — core mechanics, rules, or process
- One contextual deep-dive — choose what fits (History, Structure, Key Players, etc.)

**Optional — add if genuinely valuable (up to 3):**
Economics · Culture & Impact · Controversies · Key People · Comparisons

### Interactive elements

Always include: sticky tab bar + hover tooltips on jargon.

Pick 2–3 more by topic shape:

| Topic has… | Use… |
|---|---|
| Sequence of events | Click-to-expand timeline |
| Parallel comparable items | Card grid |
| Process or lifecycle | Phase/step flow |
| Rules, FAQs, dense lists | Collapsible accordion |
| Key statistics | Animated counters (scroll-triggered) |

### Cognitive rules (non-negotiable)

- **Inverted pyramid** — most important insight is the first sentence of every section
- **Concrete before abstract** — show a real example before explaining the concept
- **Prior knowledge bridge** — hero opens with an analogy to something universally familiar

### Sources

- Hover tooltips on specific stats — reader never loses their place
- Dedicated Sources tab — full URL list at the end
- Source priority: official/primary → academic/institutional → established journalism
- Every individual statistic needs a real, web-searched URL

## Advanced features

See [REFERENCE.md](REFERENCE.md) for:
- Design system (CSS custom properties to copy verbatim)
- HTML structure skeleton
- Tab switching JS pattern (copy verbatim — this is the bug-prone one)
- Common mistakes and pre-handover checklist
