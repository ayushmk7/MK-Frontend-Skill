# MK frontend design language

This is the design reference for MK interfaces. The identity is **black and white, one royal blue accent, Allo type, and the BB8 light/dark switch**. Use the same visual language on landing pages, dashboards, workspaces, and component libraries.

## Core identity

- Use white or near-white pages in light mode and black or near-black pages in dark mode. Neutrals carry the layout; blue marks action, selection, links, and focus.
- Use **royal blue `#2563EB` (blue-600) as the only UI blue**, in both appearances and on every page. Blue fills carry white text. Small links on black use neutral light text with a persistent underline because `#2563EB` does not reach normal-text contrast there.
- Default to the system appearance. When the user chooses light or dark with BB8, save that explicit choice and apply it before the next paint. The toggle must show the effective mode, work with keyboard and assistive technology, and retain its visible focus ring. Use the original BB8 artwork and its cursor hover behavior. Its day/night illustration keeps its original sky and orange colors; those are artwork, not UI accents.
- On landing pages and websites, the header and hero together fill at least the first visible viewport on every device; the next section starts below the fold. Keep the hero's message and action visible and let short screens scroll when content cannot fit. In dark mode, use flat, opaque black boxes with thin borders. Do not add gradients, grain, blur, box shadows, glow, or hover lift. Preserve the original BB8 illustration's shading.
- Do not use eyebrows, overlines, preheading labels, or decorative section numbers anywhere. Start sections with the actual heading. Keep labels only where they identify controls or data.
- Give text, blue actions, muted text, and focus indicators readable contrast in both modes. Use semantic colors for success and errors, rather than assigning those meanings to brand blue.

## Design principles

- **One clear focal point.** Let the actual work, a product preview, or a useful result carry the screen. Use blue for the main action or selection; keep navigation and supporting controls quiet.
- **Keep each decision focused (Hick’s law).** Choice takes longer as the visible set grows. Show the options needed for the current task, group larger sets under clear names, and reveal secondary choices when needed. Keep essential actions easy to find; do not hide them in an unlabeled “more” menu.
- **Specific content before decoration.** A hero should show or describe what this product does. Remove generic claims, filler graphics, emoji labels, and visuals that compete with the product.
- **Hierarchy through size and space.** Make headings, body copy, controls, and data easy to scan. Keep small text at normal or slightly open tracking; reserve tight tracking for large display type. Use uppercase sparingly for headings, never as a decorative preheading.
- **No dropdowns.** Select menus hide choices and add a step. Show small sets as labeled buttons; split larger sets into named views and offer search when needed. Keep the current choice visible.
- **Repeat decisions.** Components with the same job share dimensions, padding, border treatment, and interaction states. Vary size only when the content or hierarchy calls for it.
- **Separate with space.** Do not add decorative rules between sections, metadata, activity items, resource links, or table rows. Use spacing and alignment to group content. Keep borders where they define a card or control or show keyboard focus. Add table rules only when dense data cannot be read clearly without them.
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

For landing pages and websites, size the hero to the visible viewport minus the header, using `100svh` where supported. Center its content within that space, then allow the section to grow if the text or controls need more room. Check both wide and narrow screens, including short landscape viewports; never clip the message or action to force a one-screen fit.

## Base web tokens

Use these values across MK web pages. Cards are white in light mode and black in dark mode; gray belongs to text and borders, not filled boxes.

```css
:root {
  color-scheme: light;
  --mk-bg: #fafafa;
  --mk-surface: #fff;
  --mk-fg: #0a0a0a;
  --mk-muted: #4a4a4a;
  --mk-line: #d0d0d0;
  --mk-outline: #0a0a0a;
  --mk-accent: #2563eb;
  --mk-link: #2563eb;
  --mk-on-accent: #fff;
}
:root[data-mode="dark"] {
  color-scheme: dark;
  --mk-bg: #080808;
  --mk-surface: #000;
  --mk-fg: #f5f5f5;
  --mk-muted: #b7b7b7;
  --mk-line: #3a3a3a;
  --mk-outline: #888;
  --mk-link: #f5f5f5;
}
```

Use opaque fills and a quiet border to define each box. Never use gray filled cards, gradients, blur, or shadows.

## One system across page types

Use Allo Variable Friendly with a system sans fallback, the same palette, 20px card corners, curved outlined actions, and BB8 on every page. Adapt content order and density to the task: a landing page opens with its full-viewport hero; a dashboard leads with useful metrics and data; a workspace gives its editor room; a component library groups related examples. These are page types, not separate visual themes.

## Allo reading stack

| Role | Weight | Size | Line height | Tracking |
| --- | --- | --- | --- | --- |
| Hero display | 800 | `clamp(3.1rem, 7vw, 7.5rem)`; scale to about 32–40px on phones | 1.06 | 0 |
| Page title | 800 | `clamp(2.6rem, 5vw, 4.2rem)` | 1.07 | `-0.015em` |
| Section or card title | 800 | 20–28px | 1.2–1.25 | 0 |
| Body copy | 400 | 16–19px | 1.55–1.65 | 0 |
| Action or control | 700 | 13–14px | At least 1.3 | 0 |

Allo's heavy weights and tightly packed shapes make extra negative tracking hard to read. Keep the hero at weight 800 with neutral tracking and room between lines. Limit body copy to a comfortable line length, and let headings wrap before reducing type below a readable size. Use `font-synthesis: none` so fallback styling does not invent heavier glyphs.

## Component grammar

| Element | MK treatment |
| --- | --- |
| Primary action | One prominent blue fill with white text; immediate press feedback |
| Secondary action | Neutral surface or transparent fill with a visible border |
| Link | Blue text in light mode; underlined neutral text in dark mode for readable contrast |
| Card or panel | Opaque black in dark mode and white in light mode; 20px radius and consistent inner spacing; never a gray fill |
| Short stats or key facts | Center each label-and-value group horizontally and vertically; separate groups with space, without an enclosing rule or dividers |
| Filter or tab | Capsule; selected state is visible through fill, text, and `aria-pressed` or `aria-selected` |
| Navigation and choice sets | Group destinations by task; show the current choice and one clear primary action. Use visible buttons for short filters, and named views plus search for longer sets |
| Dropdown | Do not use dropdowns or select menus for navigation, filters, appearance, or actions; keep choices visible in buttons or named views |
| Form field | Visible label, useful placeholder, clear focus state, accessible error text |
| Data table | Clear heading hierarchy, aligned columns, tabular numbers, space between rows, and internal horizontal scroll on mobile; no default row rules |
| Theme switch | Existing BB8 art with a focusable checkbox/button, correct effective state, reduced-motion support |

Make every action button a curved brutalist pill with a 2px outline. Keep the blue primary fill and neutral secondary fill flat; use contrast, type, and borders for character instead of shadows or raised effects.

## Motion and usability

[Ken's resources page](https://kenisbuilding.com/resources) is a reference for motion choices. Select the few principles that support a screen rather than showing a full catalogue or a "browse all" accordion in the interface. Apply these defaults:

- Press and hover feedback: **100–150ms**. Ordinary UI moves: **150–300ms**. Large panels: up to **400ms**. Closing should be faster than opening.
- Stagger only the first few list items, by **30–60ms**, keeping the whole reveal under about **300ms**.
- Make menus or panels appear from their trigger, keep motion interruptible, and show click feedback within **100ms**.
- Keep frequent actions calm. Give one primary action visual emphasis. Preserve 44px touch targets where possible.
- Honor `prefers-reduced-motion`, reduced transparency, high contrast, keyboard focus, and system appearance changes.

Use a motion technique only where it clarifies feedback or orientation. Do not squash text or animate data just to show off.

## Before shipping an MK screen

Inspect the rendered screen first, then write down its product, character, material, main moment, and one signature detail. Fix spacing across the whole screen before tuning color, icons, copy, type, layout, details, visuals, and motion. Preserve existing features and content unless the task calls for a change.

- [ ] On landing pages and websites, the header and hero fill the first visible viewport at desktop and mobile sizes; the hero has a specific product message and no more than one primary and one secondary action.
- [ ] Repeated elements share dimensions; spacing follows the 4px grid and related items sit closer together than separate groups.
- [ ] Each step exposes a small, relevant choice set; larger libraries and filters are grouped with clear labels, essential actions stay visible, and there are no dropdowns.
- [ ] Blue appears only where it carries action or state; dark boxes remain opaque black without grain, gradients, blur, or shadows.
- [ ] Decorative divider lines are absent; borders serve a clear component, focus, or data-reading purpose.
- [ ] There are no eyebrows, decorative preheadings, or filler visuals.
- [ ] Light, dark, keyboard focus, BB8 state, reduced motion, reduced transparency, and high contrast have been checked.
- [ ] Mobile has no page overflow; dense tables scroll within themselves; copy and data remain readable.

Compare the screen before and after the pass at desktop and mobile sizes. **Spacing and review structure adapted from [Unslop](https://github.com/heydamir/unslop) by Damir Sokolovsky, licensed [CC BY 4.0](https://github.com/heydamir/unslop/blob/main/LICENSE).** MK's palette, BB8, unified page language, and no-eyebrow rule remain this project's own direction.

