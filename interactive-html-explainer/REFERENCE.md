# Interactive HTML Explainer — Reference

## Design system

Copy verbatim, then adjust `--primary` and `--accent` to the topic's brand colors (team colors, flag colors, company palette, etc.).

```css
:root {
  --primary: #17408B;
  --accent:  #C9082A;
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

Dark background always.

## HTML structure skeleton

```html
<!DOCTYPE html>
<html lang="en">
<head><!-- meta, title, <style> with full CSS --></head>
<body>
  <header class="hero">       <!-- gradient, title, prior-knowledge analogy, badge -->
  <nav class="tab-bar">       <!-- sticky tab buttons, one per section -->
  <section class="section active" id="tab-overview">
  <section class="section" id="tab-how-it-works">
  <section class="section" id="tab-[deep-dive]">
  <!-- optional sections -->
  <section class="section" id="tab-sources">
  <footer>
  <script>                    <!-- tab switching + interactive element logic -->
</body>
</html>
```

## Tab switching (copy verbatim)

Forgetting to deactivate all tabs before activating the new one is the most common bug — use this exact pattern:

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

## Common mistakes

| Mistake | Fix |
|---------|-----|
| Using Bootstrap/Tailwind CDN | All CSS inline — no network requests |
| Leading with definition, not insight | Inverted pyramid: most important thing first |
| Abstract explanation before example | Concrete first, always |
| Inventing statistics | Web search every number before using it |
| Too many interactive widgets | 2–3 beyond the tab bar max |
| Generic dark colors | Tie `--primary`/`--accent` to the topic's visual identity |
| Forgetting mobile | `clamp()` for font sizes; `flex-wrap` for grids |

## Pre-handover checklist

- [ ] Every statistic has a real source URL (hover tooltip + Sources tab)
- [ ] Each section opens with its most important insight (inverted pyramid)
- [ ] Hero contains a prior-knowledge analogy
- [ ] At least one concrete example precedes each abstract concept
- [ ] Interactive elements match topic shape (not copied from a previous example)
- [ ] Tab switching uses the exact pattern above
- [ ] No external URLs in `<link>` or `<script src>` tags
