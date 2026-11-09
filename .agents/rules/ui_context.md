# HireUS-Tools: UI Context

Read this before building or changing any screen. Every feature must follow it so the whole product looks like one design.

## Rules

1. Never hard-code hex values, radii, or font sizes in components. Use the tokens below.
2. Use the documented app shell, components, and patterns. Do not invent new layouts, shades, shadows, or accent colors. Never float, gap, or round the three app-shell columns.
3. One warm accent family only (ember). No blue, green, or purple UI colors.
4. The thermal gradient is a highlight: at most one per screen section (a thermal button counts).
5. Placeholder content stays obviously a placeholder (`[Candidate name]`, `[XX]%`). Never invent stats, logos, or testimonials.
6. Every screen must work with Vietnamese text (see Typography).
7. Status colors (success/error/warning) are not defined. Convey status with an icon, a text label, and `--charred-ash`; do not use ember colors for errors. Do not introduce new colors without asking.

## Look and feel

Warm-minimal SaaS with a thermal glow: airy, large type, soft rounded cards, hairline borders, no hard shadows. Swiss-style details: small uppercase labels, numbered section labels like `(01) Candidates`.

## Color tokens

| Token | Hex | Use |
|---|---|---|
| `--ash-white` | `#FFFBF7` | Page and panel background |
| `--surface` | `#F4EFEA` | App canvas behind panels, default cards, chips |
| `--soft-ember` | `#FDEBD6` | Selected rows, active nav item, subtle tags |
| `--spark-ash` | `#F9D9B0` | Avatars, gradient top, soft highlights |
| `--glowing-cinder` | `#F2934D` | Mid-gradient, hover glow |
| `--blazing-ember` | `#E85D2C` | Primary accent: active tab underline, large shapes |
| `--ember-core` | `#C1341A` | Active icon/text on Soft Ember, gradient base, surfaces carrying small white text |
| `--coal` | `#8A2B25` | Pressed/hover on ember surfaces |
| `--charred-ash` | `#2B1210` | Primary text, primary button background |
| `--muted-ash` | `#6E5A53` | Secondary text, captions, inactive nav |
| `--hairline` | `#EADFD6` | 1px dividers and container borders |
| `--border` | `#E3D6CB` | Outlined buttons, input borders |
| `--heat-yellow` | `#FAC76B` | Thermal gradients only |

```css
:root {
  --ash-white: #FFFBF7;  --surface: #F4EFEA;  --soft-ember: #FDEBD6;
  --spark-ash: #F9D9B0;  --glowing-cinder: #F2934D;  --blazing-ember: #E85D2C;
  --ember-core: #C1341A; --coal: #8A2B25;  --charred-ash: #2B1210;
  --muted-ash: #6E5A53;  --hairline: #EADFD6;  --border: #E3D6CB;
  --heat-yellow: #FAC76B;
}
```

If the project uses Tailwind, map these exact names and values into `theme.extend.colors`.

## Thermal gradient

Layered radial gradients over a solid `--ember-core` base, softened with `filter: blur()`. Put it on an absolutely positioned child (`inset: -30px`) inside a container with `overflow: hidden`, behind the content (content gets `position: relative`). Decorative: `aria-hidden="true"`. Text on it is white, weight 500+, and sits on the `--ember-core` (bottom) end.

```css
/* Cards, stat cells, summary panels (blur 16px) */
--heat-bg:
  radial-gradient(70% 45% at 75% 12%, #F9D9B0 0%, transparent 100%),
  radial-gradient(80% 40% at 25% 38%, #F2934D 0%, transparent 100%),
  radial-gradient(90% 30% at 60% 56%, #E85D2C 0%, transparent 100%),
  #C1341A;

/* Marketing hero orb (circle, blur 14px) + halo (same circle, opacity .4, blur 70px) */
--orb-bg:
  radial-gradient(circle at 24% 20%, #C1341A 0%, transparent 34%),
  radial-gradient(circle at 80% 86%, #FAC76B 0%, transparent 56%),
  radial-gradient(circle at 40% 38%, #E85D2C 0%, transparent 64%),
  #F2934D;
--orb-halo: radial-gradient(circle at 50% 50%, #E85D2C 0%, transparent 70%);

/* Marketing CTA banner (blur 30px, bright areas in corners) */
--banner-bg:
  radial-gradient(45% 90% at 4% 0%, #F2934D 0%, transparent 70%),
  radial-gradient(45% 80% at 100% 100%, #FAC76B 0%, transparent 70%),
  radial-gradient(55% 100% at 96% 0%, #E85D2C 0%, transparent 70%),
  #C1341A;
```

In the app, use `--heat-bg` only, for one featured element per screen (a summary card, a key stat, a selected/featured card).

### Thermal buttons

For the single primary CTA on a screen (for example "Schedule interview") or the marketing hero button. A thermal button counts as the section's one thermal element, so don't pair it with a thermal card in the same section.

```css
--heat-btn:
  radial-gradient(45% 110% at 0% 0%, #E85D2C 0%, transparent 70%),
  radial-gradient(40% 100% at 100% 100%, #F2934D 0%, transparent 70%),
  #C1341A;

.btn-thermal {
  position: relative; isolation: isolate; overflow: hidden;
  height: 44px; padding: 0 24px; border: 0; border-radius: 999px;
  background: #C1341A; color: #fff; font: 600 14px/1 Inter, system-ui, sans-serif; cursor: pointer;
}
.btn-thermal::before {
  content: ""; position: absolute; inset: -10px; z-index: -1;
  background: var(--heat-btn); background-size: 130% 130%; background-position: 0% 0%;
  filter: blur(8px);
  transition: background-position .45s ease, background-size .45s ease;
}
.btn-thermal:hover::before { background-position: 100% 100%; background-size: 160% 160%; }
.btn-thermal:active { filter: brightness(.9); }
.btn-thermal:focus-visible { outline: 2px solid var(--charred-ash); outline-offset: 3px; }
@media (prefers-reduced-motion: reduce) { .btn-thermal::before { transition: none; } }
```

Hover behavior: the glow drifts and swells across the button over ~450ms. No color swap, no lift, no opacity change. Keep the light blobs at the edges so the centered white label stays on `--ember-core` (contrast at least 4.5:1); don't enlarge them beyond the values above. Pressed: `brightness(.9)`. Disabled: static layer, 40% opacity, no hover animation. Only animate `background-position` and `background-size` (never layout properties).

## Typography

Font: **Inter** (400, 500, 600), fallback `system-ui, sans-serif`.

| Style | Size / weight | Notes |
|---|---|---|
| Page title (list panel) | 24px / 500 | letter-spacing -0.02em |
| Detail title | 28px / 500 | letter-spacing -0.03em, line-height 1.15 |
| Marketing H1 | `clamp(32px, 4.2vw, 48px)` / 400 | UPPERCASE, line-height 1.12 (1.25+ for Vietnamese) |
| Marketing H2 | `clamp(28px, 3.4vw, 40px)` / 500 | letter-spacing -0.03em |
| Big number | `clamp(48px, 5.4vw, 72px)` / 400 | letter-spacing -0.04em; unit at 20px |
| Card title | 15px / 600 | |
| Body | 14px / 400-500 | line-height 1.45-1.5 |
| Caption | 13px / 400 | `--muted-ash` |
| Section label | 11px / 500 | UPPERCASE, letter-spacing 0.08em, `--muted-ash`, format `(01) Candidates`; goes above each page/section title |

Text on gradients is weight 500+.

**Vietnamese:** Inter supports it, but the Vietnamese subset must load (`subsets: ['latin', 'vietnamese']` for `next/font` or self-hosting). Uppercase Vietnamese needs line-height 1.25+ (prefer sentence case). Letter-spacing never tighter than -0.03em. Vietnamese strings run longer than English: buttons, tabs, chips, and rows must wrap or grow, never overflow. Copy lives in translation files, not in components.

## Spacing, radius, layout

- Spacing scale (px): 4, 8, 12, 16, 20, 24, 32, 40, 56, 64, 96, 120. Prefer multiples of 8.
- Radius: pills/chips/buttons `999px`; cards inside columns `22px`; table/stat containers `20px`; list rows and inner cards `14px`; inputs and nav icon buttons `12-14px`. The app-shell columns themselves have no radius.
- Borders: 1px `--hairline`. Elevation comes from color contrast, not shadows. Hover lift: `translateY(-3px)`.
- Mobile-first with flex-wrap (`flex: 1 1 <min-width>`) so rows stack by themselves. No horizontal page scroll at 360px.

## App shell (all logged-in screens): icon rail + list + detail

The three columns form **one connected, edge-to-edge frame**: no outer padding, no gaps between columns, no rounded corners on the columns, no floating panels. Build it as a full-height flex row (`display: flex; flex-wrap: wrap; gap: 1px; background: var(--hairline); min-height: 100%`), so the 1px dividers between columns come from the gap. Rail background is `--surface`; list and detail are `--ash-white`. Rounded corners apply only to elements inside the columns (rows, cards, chips, buttons).

**1. Icon rail** (left, 72px wide, full height, `--surface` background, padding `16px 13px`)
- HireUS logo mark at the top (46px target), then one 46x46 icon button per top-level section (Overview, Jobs, Candidates, Interviews, Analytics), gap 8px.
- Icons: 20px outline, stroke 1.75. Button radius 14px.
- Active: `--soft-ember` background, `--ember-core` icon. Inactive: transparent, `--muted-ash`. Hover: `filter: brightness(.95)`.
- Every button has `aria-label`; the current one has `aria-current="page"`.

**2. List column** (`flex: 1 1 320px; max-width: 420px`, `--ash-white`, padding 20px, gap 16px)
- Header: section label `(01) Candidates` above a 24px title.
- Filter chips: 32px tall pills, 13px/500. Active: `--charred-ash` bg, `--ash-white` text. Inactive: `--surface` bg, `--charred-ash` text.
- Rows: padding 12px, radius 14px, gap 12px; 40px circular avatar, name 14px/600, subline 13px `--muted-ash`, stage text 12px/500 on the right. Selected row: `--soft-ember` bg and `--spark-ash` avatar.

**3. Detail column** (`flex: 999 1 480px`, `--ash-white`, fills the remaining width, padding 28px, gap 24px)
- Header: 56px avatar, 28px title, 14px muted subline; actions on the right (one secondary pill, one primary pill).
- Tabs: 14px/500, gap 24px, 1px `--hairline` underline for the row, active tab has a 2px `--blazing-ember` underline, inactive `--muted-ash`.
- Content: flex-wrap grid, gap 16px. Cards are radius 22px, padding 24px, min-height 220px for summary cards. Variants: **featured** (thermal `--heat-bg`, white text, one per screen), **default** (`--surface`), **outlined** (1px `--hairline`, for long content like experience or notes).

**Responsive:** columns wrap; below ~900px the list column goes full width above the detail column, and the rail becomes a horizontal row of icons. The 1px dividers stay between the stacked sections.

**Screens that are not list+detail** (dashboards, tables, forms, settings): keep the rail and the same connected frame; replace the list and detail columns with a single full-width `--ash-white` column (padding 28px, no radius), with the section label and title at the top.

**Marketing / public pages** have no rail: a top nav (logo left, centered links, "Sign in" text link and primary pill right), content in a 1280px container with 32px side padding, 120px between sections, and a footer.

## Components

- **Buttons:** pills, 44px tall, 14px/500, padding 0 20-24px. Primary: `--charred-ash` bg, `--ash-white` text. Secondary: `--ash-white` bg, 1px `--border`, `--charred-ash` text. On gradient: `--ash-white` bg, `--charred-ash` text. Thermal (primary CTA, one per section): see "Thermal buttons". Hover opacity .85 (not on thermal), disabled 40% opacity. Use `<button>` for actions and `<a>` for navigation, never a clickable `<div>`.
- **Stage pills (status of a candidate):** 26px tall, 12px/500, padding 0 12px. Applied: `--surface` / `--charred-ash`. Screening: `--soft-ember` / `--ember-core`. Interview: `--spark-ash` / `--charred-ash`. Offer: `--ember-core` / white.
- **Tags/skill chips:** 30px tall pills, `--soft-ember` bg, `--charred-ash` 13px/500.
- **Stat strip:** cells separated by a 1px `--hairline` gap inside a radius-20px container (`overflow: hidden`), cell padding 24-28px, big number plus caption. At most one cell uses `--heat-bg`.
- **Table:** container with 1px `--hairline` border, radius 20px; header row `--surface` with 11px uppercase `--muted-ash` labels; rows 14px with 1px `--hairline` top borders, padding 14px 24px. Wide tables scroll inside the container (`overflow-x: auto`).
- **Inputs:** 44px tall, radius 12px, `--ash-white` bg, 1px `--border`, 14px text, always a visible label (or `aria-label` for search). Focus: the global focus ring.
- **Icons:** Lucide or equivalent outline icons, stroke 1.75, `currentColor`, 16-22px. No emoji. Decorative icons get `aria-hidden="true"`; icon-only buttons get `aria-label`.
- **Empty / loading / error:** every data view needs all three. Loading: `--surface` skeleton blocks with the same radius as the real content. Empty: one line of `--muted-ash` text plus one primary action.

## Motion and accessibility

- Hover lift 200ms, gradient fade 350ms, button hover 150ms, thermal button glow drift 450ms. Respect `prefers-reduced-motion`.
- Keyboard focus ring everywhere: 2px solid `--charred-ash`, 3px offset, never removed. Touch targets at least 44px (rail buttons are 46px).
- Contrast: small white text only on `--ember-core` (about 5.6:1) or `--coal`; `--charred-ash` on `--glowing-cinder`, `--spark-ash`, or `--soft-ember`; `--muted-ash` on `--ash-white`/`--surface` is about 6:1. White on `--blazing-ember` is about 3.5:1, so only for text 24px or larger.
- Never convey meaning with color alone. Images need alt text; decorative visuals use `alt=""` or `aria-hidden`.
