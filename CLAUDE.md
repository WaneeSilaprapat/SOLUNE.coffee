# Coffepage — CLAUDE.md

Single-file HTML/CSS/JS landing page for a Thai premium coffee delivery brand.
Reference details: `project_brief_coffee_website.md`

## Working Modes

Activate by saying **"Save Mode"** or **"Full Auto"** at the start of a message.
Default is **Save Mode** unless told otherwise.

### Save Mode (default)
- No agent spawning. Use Read, Edit, Bash directly.
- Targeted file reads only.
- Work on one section at a time.
- Short responses. No trailing summaries.

### Full Auto Mode
- Spawn parallel agents for cross-section work.
- Full exploration allowed.
- Validate mobile layout, animation performance, and CTA visibility after every change.
- Auto-escalate to Full Auto whenever a change touches the color palette or typography tokens.

## Architecture Rules (never break these)

1. **Everything lives in one file: `index.html`** — embedded `<style>` and `<script>`, no external JS bundles.
2. **CTA ("สั่งซื้อเลย") must be visible within 1 second** — never hidden behind animations or lazy loading.
3. **Animations must never block the order button.** `pointer-events: none` on all decorative animations.
4. **Color tokens defined once in `:root` CSS variables** — never hardcode HEX values outside `:root`.
5. **Mobile-first CSS** — base styles for 360px, media queries scale up to 768px and 1280px.
6. **Images use Unsplash source URLs** until real photos are provided. Always include `loading="lazy"` except the hero image.
7. **Delivery platform links are clearly marked `<!-- TODO: replace with real link -->`**.
8. **Typography loaded from Google Fonts** — Playfair Display + IBM Plex Sans Thai + Inter.

## CSS Token Contract (never change variable names)

```css
:root {
  --color-forest:     #2D4A2B;
  --color-sage:       #8AA68B;
  --color-rose:       #D4A5A0;
  --color-cream:      #F5F1E8;
  --color-warm-white: #FAF7F0;
  --color-charcoal:   #3A3530;
  --color-walnut:     #7A5C42;
  --font-display:     'Playfair Display', serif;
  --font-thai:        'IBM Plex Sans Thai', sans-serif;
  --font-body:        'Inter', sans-serif;
}
```

## Section Contract (6 sections, in order)

| ID | Section | Critical rule |
|----|---------|---------------|
| `#hero` | Hero | 100vh, CTA visible < 1s, animation non-blocking |
| `#story` | Our Story | Fade-in on scroll |
| `#beans` | Our Beans | 3 interactive cups (light/medium/dark roast) |
| `#menu` | Menu | 6 cards with name, description, price, order link |
| `#order` | Order Now | 3 platform buttons (Grab / LINE MAN / Shopee) |
| `#footer` | Footer | Social links, copyright |

## Banned patterns

```
position:fixed on animations   → use position:absolute inside bounded containers
JS-driven hero animation        → use CSS @keyframes only (performance)
hardcoded color HEX in CSS      → use var(--color-*) only
missing alt text on images      → every <img> must have descriptive alt
```
