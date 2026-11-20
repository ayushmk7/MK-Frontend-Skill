# MK frontend design language

This is the design reference for MK interfaces. The common identity is **black and white, one royal blue accent, and the BB8 light/dark switch**. The same identity can be loud on a portfolio and quiet in a tool. Keep an existing product's visual treatment when extending it.

## Core identity

- Use white or near-white pages in light mode and black or near-black pages in dark mode. Neutrals carry the layout; blue marks action, selection, links, and focus.
- Use **royal blue `#2563EB` (blue-600) as the only UI blue**, in both appearances and every expression. Blue fills carry white text. Small links on black use neutral light text with a persistent underline because `#2563EB` does not reach normal-text contrast there.
- Default to the system appearance. When the user chooses light or dark with BB8, save that explicit choice and apply it before the next paint. The toggle must show the effective theme, work with keyboard and assistive technology, and retain its visible focus ring. Use the original Website BB8 artwork and its cursor hover behavior. Its day/night illustration keeps its original sky and orange colors; those are artwork, not UI accents.
- Lead with the hero before theme choices or supporting content. In dark mode, use flat, opaque black boxes with thin borders. Do not add gradients, grain, blur, box shadows, glow, or hover lift. Preserve the original BB8 illustration's shading.
- Do not use eyebrows, overlines, preheading labels, or decorative section numbers anywhere. Start sections with the actual heading. Keep labels only where they identify controls or data.
- Give text, blue actions, muted text, and focus indicators readable contrast in both modes. Use semantic colors for success and errors, rather than assigning those meanings to brand blue.

## Design principles

- **One clear focal point.** Let the actual work, a product preview, or a useful result carry the screen. Use blue for the main action or selection; keep navigation and supporting controls quiet.
- **Specific content before decoration.** A hero should show or describe what this product does. Remove generic claims, filler graphics, emoji labels, and visuals that compete with the product.
- **Hierarchy through size and space.** Make headings, body copy, controls, and data easy to scan. Keep small text at normal or slightly open tracking; reserve tight tracking for large display type. Website's uppercase display type is a deliberate brand exception, not a pattern for small labels.
- **Repeat decisions.** Components with the same job share dimensions, padding, border treatment, and interaction states. Vary size only when the content or hierarchy calls for it.
- **Motion explains change.** Hover, press, menus, and panels should acknowledge an action or preserve orientation. Avoid looping decoration, bounce, parallax, and movement that makes repeated work tiring.

## Spacing and layout

Work on a **4px grid** for margins, padding, gaps, and fixed heights. Start with `4, 8, 12, 16, 20, 24, 32, 40, 48, 64, 80, 96, 128px`; other multiples of 4 are valid when the layout needs them. A 2px optical correction inside a small control is acceptable; one-off values elsewhere need a reason.

| Relationship | Starting range | Application |
| --- | --- | --- |
| Inside a control | 4–12px | Keep icon-to-label gaps and control insets consistent |
| Between related items | 4–8px | Rows, chips, and items in one group; dense navigation may use 2–4px |
| Between groups | 12–24px | A card's text, actions, and adjacent card groups |
| Between app sections | 32–64px | Separate tasks without making a tool feel sparse |
| Between landing sections | 80–128px | Give the hero and major stories room to breathe |
| Page edge | 24–32px desktop; 16–24px mobile | Align sections to one shared gutter |
| Navigation to hero headline | 96–128px desktop; 48–64px mobile | Apply to stacked heroes; center a split hero against its visual |

Use about 16px padding for compact panels and 20–24px for cards. Keep repeated rows the same height: about 32–36px for compact navigation and at least 44px for touch-first actions. Space within a group must be smaller than the gap to the next group. Align icons, label starts, and numeric columns instead of correcting them with stray offsets.

Keep portfolio content near 1200px wide. Let app content stay fluid, with a practical cap around 1440–1600px. On small screens, stack content in reading order and let dense tables scroll inside their own container.

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
  --mk-surface: #000;
  --mk-fg: #f5f5f5;
  --mk-muted: #aaaaaa;
  --mk-line: rgb(255 255 255 / 14%);
  --mk-link: #f5f5f5;
}
```

Use an opaque fill and a hairline to define each box. Keep the chosen expression's neutral colors and component conventions when extending an existing interface.

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
| Card or panel | Opaque black in dark mode, white or near-white in light mode; expression-specific radius and consistent inner spacing |
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

Inspect the rendered screen first, then write down its product, character, material, main moment, and one signature detail. Fix spacing across the whole screen before tuning color, icons, copy, type, layout, details, visuals, and motion. Preserve existing features and content unless the task calls for a change.

- [ ] The hero leads with a specific product message and no more than one primary and one secondary action.
- [ ] Repeated elements share dimensions; spacing follows the 4px grid and related items sit closer together than separate groups.
- [ ] Blue appears only where it carries action or state; dark boxes remain opaque black without grain, gradients, blur, or shadows.
- [ ] There are no eyebrows, decorative preheadings, or filler visuals.
- [ ] Light, dark, keyboard focus, BB8 state, reduced motion, reduced transparency, and high contrast have been checked.
- [ ] Mobile has no page overflow; dense tables scroll within themselves; copy and data remain readable.

Compare the screen before and after the pass at desktop and mobile sizes. **Spacing and review structure adapted from [Unslop](https://github.com/heydamir/unslop) by Damir Sokolovsky, licensed [CC BY 4.0](https://github.com/heydamir/unslop/blob/main/LICENSE).** MK's palette, BB8, expressions, and no-eyebrow rule remain this project's own direction.

