# MK frontend design language

This is the design reference for MK interfaces. The common identity is **black and white, one royal blue accent, and the BB8 light/dark switch**. The same identity can be loud on a portfolio and quiet in a tool. Keep an existing product's visual treatment when extending it.

## The rules that stay the same

- Use white or near-white pages in light mode and black or near-black pages in dark mode. Neutrals carry the layout; blue marks action, selection, links, and focus.
- Use **royal blue `#2563EB` (blue-600) as the only UI blue**, in both appearances and every expression. Blue fills carry white text. Small links on black use neutral light text with a persistent underline because `#2563EB` does not reach normal-text contrast there.
- Default to the system appearance. When the user chooses light or dark with BB8, save that explicit choice and apply it before the next paint. The toggle must show the effective theme, work with keyboard and assistive technology, and retain its visible focus ring. Use the original Website BB8 artwork and its cursor hover behavior. Its day/night illustration keeps its original sky and orange colors; those are artwork, not UI accents.
- Use the `4, 8, 12, 16, 24, 32px` spacing scale. Align content to a shared grid; keep web content roughly 1200px wide and let dense tables scroll within their own container on small screens.
- Lead with the hero before theme choices or supporting content. In dark mode, use plain translucent black glass for boxes, with a thin border and blur; use solid black when reduced transparency or high contrast is requested. Do not add gradients, box shadows, glow, or hover lift. Preserve the original BB8 illustration's shading.
- Do not use eyebrows, overlines, preheading labels, or decorative section numbers anywhere. Start sections with the actual heading. Keep labels only where they identify controls or data.
- Give text, blue actions, muted text, and focus indicators readable contrast in both modes. Use semantic colors for success and errors, rather than assigning those meanings to brand blue.

## Base web tokens

These are the starting values for **new MK web work**. When extending an existing product, retain its component conventions while normalizing its blue UI accents to `#2563EB`.

```css
:root {
  color-scheme: light;
  --mk-bg: #fff;
  --mk-surface: #f5f5f5;
  --mk-fg: #0a0a0a;
  --mk-muted: #4a4a4a;
  --mk-line: rgb(0 0 0 / 10%);
  --mk-accent: #2563eb;
  --mk-link: #2563eb;
  --mk-on-accent: #fff;
}
html.dark {
  color-scheme: dark;
  --mk-bg: #000;
  --mk-surface: #141414;
  --mk-fg: #f5f5f5;
  --mk-muted: #aaaaaa;
  --mk-line: rgb(255 255 255 / 14%);
  --mk-link: #f5f5f5;
}
```

## Three MK expressions

| Expression | Type | Surfaces and controls | Use for |
| --- | --- | --- | --- |
| **Website / graphic** | Archivo Black uppercase display, DM Sans body, Space Grotesk controls, JetBrains Mono small labels | Strong outlines, rounded section sheets, flat panels, pill actions | Portfolios, launches, editorial showcases |
| **Internship / utility** | System sans, compact semibold hierarchy | Flat black/white canvas, hairline borders, blue active pills | Search, filters, tables, dashboards |
| **Virgule / native** | Platform system sans and monospace for code | Dynamic system colors, quiet panels, hairline dividers, capsule actions, compact density | Desktop tools and document workspaces |

Choose one expression for a screen. Share the palette, spacing, BB8 behavior, and interaction rules across them. Keep each screen's type, outlines, and panel density consistent.

## Component grammar

| Element | MK treatment |
| --- | --- |
| Primary action | One prominent blue fill with white text; immediate press feedback |
| Secondary action | Neutral surface or transparent fill with a visible border |
| Link | Blue text in light mode; underlined neutral text in dark mode for readable contrast |
| Card or panel | Translucent black glass in dark mode, white or near-white in light mode; expression-specific radius and consistent inner spacing |
| Filter or tab | Capsule; selected state is visible through fill, text, and `aria-pressed` or `aria-selected` |
| Form field | Visible label, useful placeholder, clear focus state, accessible error text |
| Data table | Clear heading hierarchy, tabular numbers, row separators, internal horizontal scroll on mobile |
| Theme switch | Existing BB8 art with a focusable checkbox/button, correct effective state, reduced-motion support |

Cyberpunk, brutalist, vaporwave, and Nordic are optional **style studies**. They explore type, borders, shape, and surface treatment while using the same black/white/gray neutrals and `#2563EB`. Their panels and controls stay flat. They are separate from the three MK expressions, not extra brand palettes.

## Motion and usability

[Ken's resources page](https://kenisbuilding.com/resources) collects five design tools and twenty motion/UX principles. Select the few principles that support a screen rather than animating every element. Apply these defaults:

- Press and hover feedback: **100–150ms**. Ordinary UI moves: **150–300ms**. Large panels: up to **400ms**. Closing should be faster than opening.
- Stagger only the first few list items, by **30–60ms**, keeping the whole reveal under about **300ms**.
- Make menus or panels appear from their trigger, keep motion interruptible, and show click feedback within **100ms**.
- Keep frequent actions calm. Give one primary action visual emphasis. Preserve 44px touch targets where possible.
- Honor `prefers-reduced-motion`, reduced transparency, high contrast, keyboard focus, and system appearance changes.

The full vocabulary on that page covers squash and stretch, anticipation, stagger, follow-through, easing, arcs, secondary action, timing, exaggerated feedback, depth, origin awareness, target size, rubber banding, choice count, distinctive emphasis, response time, interruptibility, fast closing, a clear ending, and frequency of use. Use a technique only where it clarifies feedback or orientation. Do not squash text or animate data just to show off.

### Resource shelf

The page also links to [Impeccable](https://github.com/pbakaus/impeccable), [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) and [getdesign.md](https://getdesign.md), [Vercel's web design guidelines](https://github.com/vercel-labs/agent-skills), [Chrome DevTools MCP](https://github.com/ChromeDevTools/chrome-devtools-mcp), and [img2threejs](https://github.com/img2threejs/img2threejs). Treat them as optional references and checks. This repo does not install them; the design language above is the source of truth.

## Before shipping an MK screen

Check light and dark mode, the chosen blue's contrast, BB8 state and keyboard focus, mobile overflow, readable copy, and reduced-motion behavior. Compare the affected screens side by side for typography, spacing, controls, and surface treatment.

