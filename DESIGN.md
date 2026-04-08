# Cortex Design System

> Visual reference: `/public/brand/system.html` (open in browser for full mockups with light/dark toggle)
> Vector icon preview: `/public/brand/icons/vector-preview.html`

## Logo & Icon

### Files (in `/public/brand/final/`)
- `cortex-mark.svg` — Neural asterisk mark only, no background (512x512)
- `cortex-app-icon.svg` — App icon with dark rounded rect background (512x512)
- `favicon.svg` — Favicon optimized (32x32)
- `cortex-wordmark.svg` — Mark + "cortex" text lockup

### Mark: Neural Asterisk
8 tapered gold rays radiating from center. Each ray is a triangle: apex 170px from center, base 24px wide, extending 6px past center so rays overlap cleanly. SVG uses `<use>` with `rotate(n, 256, 256)` transforms at 45-degree intervals.

### Wordmark Font: Newsreader
- Google Font: `Newsreader` (has optical size variants for small text)
- Weight: 400
- Lowercase "cortex"
- Distinct from Fraunces (heading font) — Newsreader is sharper/editorial, Fraunces is warmer/variable
- Use at 20px in sidebar, larger for marketing

### Sidebar Logo
- Mark: 36px x 36px, no border-radius (the rays need the full square)
- Gap: 2px between icon and text
- Text: "cortex" in Newsreader 22px, weight 400, `var(--text-headline)`
- Flex row, align-items center
- The SVG mark should be inline (not an `<img>`) so the gold color can be themed via CSS if needed

### SVG Mark Inline Code
```html
<svg viewBox="0 0 512 512" width="36" height="36">
  <defs><polygon id="ray" points="256,86 244,262 268,262" fill="#D4A843"/></defs>
  <use href="#ray" transform="rotate(0,256,256)"/>
  <use href="#ray" transform="rotate(45,256,256)"/>
  <use href="#ray" transform="rotate(90,256,256)"/>
  <use href="#ray" transform="rotate(135,256,256)"/>
  <use href="#ray" transform="rotate(180,256,256)"/>
  <use href="#ray" transform="rotate(225,256,256)"/>
  <use href="#ray" transform="rotate(270,256,256)"/>
  <use href="#ray" transform="rotate(315,256,256)"/>
</svg>
```

For smaller contexts (e.g. mobile sidebar, compact header), scale down to 24px icon / 18px text with 2px gap.

### Favicon
Use `favicon.svg` — simplified ray proportions for 16-32px rendering.

### Nav Bar (Landing/Marketing)
- Mark: 36px x 36px
- Gap: 2px
- Text: Newsreader 22px, weight 400, white
- Flex row, align-items center

## Brand Direction

**Dark editorial minimalism. Gold as the only voice in the room.**

The UI is monochrome. Gold (#D4A843) is the signal color. The AI-generated illustrated concept cards bring all other color. The chrome never competes with the content.

## Color Tokens

### Dark Mode (Default, Brand Mode)

```css
--bg: #1a1a1a;
--bg-sidebar: #161616;
--bg-card: #222222;
--bg-card-hover: #2a2a2a;
--border: #2a2a2a;
--border-hover: #333333;
--bg-overlay: rgba(0,0,0,0.5);
--bg-detail-panel: #1e1e1e;

--text-headline: #ffffff;
--text-body: #e8e8e8;
--text-secondary: #aaaaaa;
--text-muted: #888888;
--text-structural: #666666;
--text-faint: #555555;
--text-ghost: #444444;

--gold: #D4A843;
--gold-hover: #E4B853;
--gold-bg: rgba(212, 168, 67, 0.08);
--gold-glow: rgba(212, 168, 67, 0.4);

--card-shadow: 0 8px 32px rgba(0,0,0,0.3), 0 2px 8px rgba(0,0,0,0.2);
--card-shadow-sm: 0 2px 8px rgba(0,0,0,0.2);
```

### Light Mode

```css
--bg: #FAF7F2;
--bg-sidebar: #f0ebe4;
--bg-card: #ffffff;
--bg-card-hover: #f5f2ed;
--border: #e8e4dc;
--border-hover: #d8d4cc;
--bg-overlay: rgba(0,0,0,0.15);
--bg-detail-panel: #ffffff;

--text-headline: #1a1a1a;
--text-body: #3a3a3a;
--text-secondary: #777777;
--text-muted: #999999;
--text-structural: #aaaaaa;
--text-faint: #bbbbbb;
--text-ghost: #cccccc;

--gold: #B8922E;
--gold-hover: #A07D20;
--gold-bg: rgba(184, 146, 46, 0.08);
--gold-glow: rgba(184, 146, 46, 0.3);

--card-shadow: 0 2px 12px rgba(0,0,0,0.06), 0 1px 4px rgba(0,0,0,0.04);
--card-shadow-sm: 0 1px 4px rgba(0,0,0,0.06);
```

## Typography

### Fonts
- **Headings:** Fraunces (variable serif, Google Fonts), weight 400
- **Body:** Inter (sans-serif, Google Fonts), weight 300-500

### Scale
| Role | Font | Size | Weight | Color |
|------|------|------|--------|-------|
| H1 | Fraunces | 48px | 400 | --text-headline |
| H2 | Fraunces | 32px | 400 | --text-headline |
| H3 | Fraunces | 22px | 400 | --text-headline |
| Body | Inter | 15px | 300 | --text-body |
| Meta | Inter | 13px | 400 | --text-muted |
| Label | Inter | 11px | 600 | --text-structural |

### Label Pattern (Signature Element)
```css
font-size: 11px;
font-weight: 600;
letter-spacing: 3px;
text-transform: uppercase;
color: var(--text-structural);
```
Used for section headers, category labels, and structural wayfinding throughout the app.

### Search Bar
```css
font-family: 'Fraunces', serif;
font-style: italic;
font-weight: 400;
font-size: 28px;
color: var(--text-faint);
```

## Spacing

- Between major sections: 120px
- Inside containers/cards: 48px (large), 24px (medium), 16px (small)
- Between cards in grid: 20px
- Border radius: 16px (large containers), 12px (cards), 8px (buttons/inputs), 20px (pills)

## Components

### Sidebar
- Background: var(--bg-sidebar)
- Width: ~200px
- Logo: "cortex" in Fraunces 20px with small gold dot
- Active nav item: gold text, gold left-border indicator (3px), subtle gold background
- Inactive nav item: --text-muted
- Bottom items (Settings, avatar): --text-structural

### Concept Cards
- Background: var(--bg-card)
- Border: 1px solid var(--border)
- Border radius: 12px
- Image area: 140px height (the AI illustrations provide all card color)
- Title: Fraunces 18px, --text-headline
- Description: Inter 13px, --text-secondary
- Tag pill: small colored dot + text, --bg-tag background, rounded

#### Placeholder Image (No AI Illustration Yet)
When a concept has no `imageUrl`, show a gradient placeholder instead of a broken image icon.

**Use the cortex's identity color as the gradient base:**
- Take the cortex dot color (e.g. Salsa = #C07A6A, BJJ = #B05A5A, Philosophy = #9A8AB0)
- Render a `linear-gradient(135deg, <color>, <color-darkened-20%>)` in the image area
- Center the neural asterisk SVG mark at 20% opacity as a watermark
- If the concept belongs to no cortex, use a neutral gradient: `linear-gradient(135deg, #333, #222)`

**Implementation:**
```tsx
// In the card component, where the image area renders:
{concept.imageUrl ? (
  <img src={concept.imageUrl} alt={concept.title} className="card-image" />
) : (
  <div
    className="card-image card-image-placeholder"
    style={{ background: `linear-gradient(135deg, ${cortexColor}, ${darken(cortexColor, 0.2)})` }}
  >
    {/* Neural asterisk at 20% opacity */}
    <svg viewBox="0 0 512 512" style={{ width: '48px', height: '48px', opacity: 0.2 }}>
      <defs><polygon id="ph" points="256,86 244,262 268,262" fill="#fff"/></defs>
      <use href="#ph" transform="rotate(0,256,256)"/>
      <use href="#ph" transform="rotate(45,256,256)"/>
      <use href="#ph" transform="rotate(90,256,256)"/>
      <use href="#ph" transform="rotate(135,256,256)"/>
      <use href="#ph" transform="rotate(180,256,256)"/>
      <use href="#ph" transform="rotate(225,256,256)"/>
      <use href="#ph" transform="rotate(270,256,256)"/>
      <use href="#ph" transform="rotate(315,256,256)"/>
    </svg>
  </div>
)}
```

The placeholder should:
- Use `display: flex; align-items: center; justify-content: center;` to center the watermark
- Never show a broken image icon or empty gray box
- Feel intentional, not broken — like the card is waiting for its illustration

### Buttons
- **Primary (gold):** background var(--gold), text var(--bg), weight 500, 8px radius
- **Secondary:** background var(--bg-card), text var(--text-secondary), border var(--border)
- **Ghost:** transparent, text var(--text-muted)
- **Outline gold:** transparent, border var(--gold), text var(--gold)

### Tag Pills
- Background: var(--bg-card) or var(--bg-tag)
- Border: 1px solid var(--border)
- Border radius: 20px
- Small colored identity dot (6px) + text in --text-secondary
- Dot colors are per-cortex (muted palette: dusty rose, sage, slate, amber, lavender, coral, sky, mint, peach, indigo)

### Inputs
- Background: var(--bg-input)
- Border: 1px solid var(--border)
- Border radius: 8px (standard), 12px (search)
- Placeholder: var(--text-faint)

### Flashcard (Learn Mode)
- Large centered card, max-width ~520px
- Image area: 400px height
- Card shadow for elevation
- "NEW" badge: gold text + gold border
- Rating buttons should use gold for selected/active states
- "Press Space to reveal" hint in --text-structural

### Stats Bar
- Background: var(--bg-card), border var(--border)
- Stat numbers: Fraunces 20px
- Streak number: var(--gold) with text-shadow glow
- Labels: Inter 12px, --text-muted

### Detail Panel (Slide-over)
- Background: var(--bg-detail-panel)
- Section labels: uppercase letter-spaced pattern
- Subheadings ("What it is", "When to use it"): var(--gold), Inter 14px weight 500
- Body text: var(--text-body), Inter 15px weight 300, line-height 1.7
- "+ Add to cortex" link: var(--gold)

## Cortex Identity Colors (Dot System)

Each cortex gets a muted color dot. These stay consistent across light/dark modes.

```css
--dot-rose: #B07A8A;
--dot-sage: #7A9A7A;
--dot-slate: #7A8A9A;
--dot-amber: #C4A03A;
--dot-lavender: #9A8AB0;
--dot-coral: #C07A6A;
--dot-sky: #6A9AB0;
--dot-mint: #6AB09A;
--dot-peach: #C09A7A;
--dot-indigo: #6A6AB0;
--dot-red: #B05A5A;
--dot-teal: #5AA0A0;
```

## What Changes from Current App

### Replacing
- **Coral accent (#E8734A)** → Gold (#D4A843)
- **Playfair Display** → Fraunces (similar serif, more personality via variable axes)
- **Light mode default** → Dark mode default
- **Colored backgrounds on UI chrome** → Monochrome chrome, only gold as accent

### Keeping
- Card-based grid layout
- Sidebar navigation structure
- "Search your brain..." concept
- AI-generated illustrations on cards
- Concept/Cortex/Learn page structure
- Dark mode toggle (but dark is now default)

### Key Principle
The UI is a neutral frame. Gold is the only accent in the chrome. The illustrated concept cards provide all other color. The chrome never competes with the content.

## Implementation Notes

- Use CSS custom properties at the `:root` level
- Toggle dark/light via `data-theme="light"` attribute on `<html>`
- Replace Playfair Display with Fraunces in next/font config
- Keep Inter as the body font
- Transition on theme switch: `background-color 0.3s ease, color 0.3s ease, border-color 0.3s ease`
- The existing Tailwind setup should use these tokens as CSS variables
- Reference `system.html` for exact visual targets per screen
