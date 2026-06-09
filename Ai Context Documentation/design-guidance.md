# Design Guidance

This is a living north-star document for the Marlowe prototype. Update it as the project evolves so future implementation choices stay aligned with the intended visual language, interaction model, and brand atmosphere.

## Current Reference

Primary reference page:
`src/pages/image-set-flex-two-once-tilt-paper-menu/index.astro`

This page currently defines the strongest project direction: a full-viewport image mosaic that behaves as both atmosphere and interface, with restrained restaurant navigation and a menu reveal interaction.

## North Star

The experience should feel like a refined restaurant website built from photographic fragments, not a conventional landing page with a hero image placed inside it.

The mosaic is the stage. Navigation, menu content, and contact details should feel laid over it with restraint. The visual language should be cinematic, tactile, slightly imperfect, and editorial.

Key qualities:

- Full-bleed and immersive.
- Dark, warm, low-lit atmosphere.
- High contrast between cream typography and dark photographic background.
- Tactile tile movement that feels hand-arranged, not mechanically animated.
- Minimal UI chrome, with navigation acting more like typographic signage.
- Editorial menu reveal rather than a standard modal or dropdown.

## Visual Structure

The current mosaic is a `4 x 5` image grid built from prepared image fragments. It should remain the dominant visual surface.

Current structural decisions:

- The mosaic fills the viewport using cover-style sizing: `width: max(100vw, calc(100svh * var(--mosaic-ratio)))`.
- The mosaic keeps its natural aspect ratio using `aspect-ratio: var(--mosaic-ratio)`.
- The parent shell uses flex centering so overflow crops evenly from the centre while resizing the browser.
- The shell has no padding, allowing the image field to sit close to the browser edge.
- The tile gap is intentionally tight: `clamp(1px, 0.16vw, 3px)`.
- The mosaic has dark internal gutters rather than obvious bright borders.

Guidance:

- Keep the mosaic centred when the viewport changes.
- Preserve image aspect ratio. Do not stretch individual image tiles.
- If full-screen coverage and full-image visibility conflict, favour full-screen coverage with centred cropping.
- Avoid large gutters unless deliberately moving away from the current immersive direction.
- Keep the mosaic edge-to-edge or near edge-to-edge. Avoid boxed hero layouts.

## Colour And Atmosphere

The palette should stay dark, warm, and low contrast outside the cream text.

Current values:

- Page/background base: `#111`.
- Mosaic gutter/background: `#181411`.
- Shell atmosphere: dark radial and linear gradients around `#070707`, `#1a1510`, and `#0b0a08`.
- Primary text: `#fff7e7`.
- Menu panel background: `rgba(255, 247, 231, 0.92)`.
- Menu panel text: `#17110d`.

Guidance:

- Use warm blacks and brown-black tones rather than neutral greys.
- Keep overlays translucent and soft; avoid hard white panels except for intentional editorial menu moments.
- Prefer cream/off-white text to pure white.
- Avoid bright accent colours unless they come from photography.
- Shadows should feel ambient and soft, not like generic UI cards.

## Typography

The current type system uses Adobe Typekit:

```html
<link rel="stylesheet" href="https://use.typekit.net/duj0xcr.css" />
```

Primary UI font:

```css
font-family: neue-haas-grotesk-display, sans-serif;
font-weight: 500;
font-style: normal;
```

Display/logo font:

```css
font-family: ivyora-display, serif;
font-weight: 400;
font-style: normal;
```

Current usage:

- Navigation, footer, labels, and menu item text use `neue-haas-grotesk-display`.
- The logo and large menu heading use `ivyora-display`.
- Header and footer text are uppercase with increased letter spacing.
- The menu heading uses tight line-height and negative letter spacing for an editorial feel.

Guidance:

- Use `neue-haas-grotesk-display` for functional, navigational, and informational text.
- Use `ivyora-display` sparingly for brand/title moments.
- Keep navigation all caps.
- Keep typography compact and intentional; avoid large blocks of paragraph copy over the mosaic.
- Avoid default system fonts unless Typekit fails to load.
- Maintain strong typographic hierarchy through scale, letter spacing, and font choice, not through heavy decoration.

## Header And Footer

The current chrome is fixed and minimal.

Header structure:

- Left: `MENU` button.
- Centre: `MARLOWE` text logo.
- Right: `BOOK TABLE` email link.

Footer structure:

- Left: `book@marlowe.co.nz`.
- Centre: address, opening note, copyright.
- Right: phone number.

Guidance:

- Keep header and footer fixed over the mosaic.
- Use a three-column layout on desktop: left / centre / right.
- Keep the centre logo visually anchored.
- Use small translucent dark backgrounds only where needed for legibility.
- Avoid heavy nav bars, solid bands, large buttons, or boxed site chrome.
- On small screens, allow footer content to stack and centre.

## Interaction Model

The core interaction is tactile image transformation rather than conventional page navigation.

Current behaviours:

- Hover/focus/click reveals a tile from image set `1` to image set `2` once.
- Revealed tiles keep their revealed image state.
- Tiles have subtle persistent tilt after reveal/interaction.
- `MENU` toggles a page-level state using `body[data-menu-open="true"]`.
- When menu opens, tiles scatter outward using per-tile CSS variables.
- The menu panel fades and scales into the centre after the tile movement begins.

Guidance:

- Motion should feel organic but deterministic. Avoid purely random runtime movement that changes every load unless there is a clear reason.
- Scatter should be asymmetric and tactile, not a uniform radial explosion.
- Keep easing expressive and physical. The current scatter uses `cubic-bezier(0.16, 0.84, 0.22, 1)`.
- Use short staggered delays for tile motion so the mosaic feels hand-loosened.
- Preserve keyboard/focus access for interactive controls.
- Respect `prefers-reduced-motion`.

## Menu Reveal Direction

The menu reveal should feel like the mosaic parts to expose something printed beneath it.

Current menu panel traits:

- Fixed centre panel.
- Cream paper-like surface.
- Dark ink text.
- Editorial title: `Food for the table`.
- Three-column menu categories on desktop.
- Single column on narrower screens.

Guidance:

- Treat menu content as editorial print material, not a generic modal.
- Keep the menu panel centred and calm while tiles move around it.
- Do not over-texturise the panel unless there is a clear asset/art-direction decision.
- Prefer concise menu samples and categories.
- If replacing placeholder menu items, keep item names short and visually balanced.

## Tile Aesthetic

The current direction moved away from obvious paper-rip texture. The successful version keeps the cutout feeling through spacing, shadows, and movement rather than fake rough borders.

Guidance:

- Keep tile gaps tight.
- Use subtle shadows to separate tiles.
- Avoid heavy paper textures, obvious jagged `clip-path` edges, or noisy overlays unless a high-quality asset is introduced.
- If a paper-cutout treatment returns, it should be asset-led or very restrained.
- The tile system should feel assembled by hand but still refined.

## Implementation Notes

Important current implementation details:

- Tile metadata is generated in Astro frontmatter.
- Image paths are derived from `public/1` and `public/2` folders.
- Per-tile CSS variables control hover tilt and menu scatter.
- Page state is controlled with `document.body.dataset.menuOpen`.
- Menu accessibility state is reflected through `aria-expanded` and `aria-hidden`.

Guidance:

- Keep per-tile movement data generated from deterministic calculations in frontmatter when possible.
- Prefer CSS variables for tile-specific transforms instead of large JS animation logic.
- Avoid introducing animation libraries until CSS becomes genuinely insufficient.
- Keep duplication experiments as separate routes while the design is evolving.
- Once a direction stabilises, consolidate repeated CSS/components to reduce drift.

## Responsive Principles

Current responsive behaviour:

- Mosaic remains centred and cover-sized.
- Footer stacks on small screens.
- Menu panel switches from three columns to one column under `760px`.
- Motion remains available but reduced under `prefers-reduced-motion`.

Guidance:

- The mosaic should remain the primary composition on all viewport sizes.
- Cropping should happen from the centre.
- Header/footer should remain readable without overpowering the imagery.
- Menu content should never require horizontal scrolling.
- Test by resizing browser width and height, not only by using preset device widths.

## Avoid

Avoid these unless intentionally changing direction:

- Generic hero-image layouts.
- Purple/blue SaaS-style gradients.
- Neutral grey backgrounds.
- Large rounded cards.
- Overly smooth or symmetrical tile motion.
- Heavy fake paper textures.
- Default font stacks as the main visual voice.
- UI that feels more like a prototype dashboard than a restaurant site.

## Open Decisions

These should be revisited as content and brand assets become available:

- Final logo asset versus text logo.
- Final menu content and whether `MENU` should reveal inline content, link to PDF, or support both.
- Whether the scatter menu interaction becomes the primary homepage behaviour.
- Whether paper/cutout texture should be reintroduced using real image assets.
- Final photography crop strategy for screens with very wide or very tall aspect ratios.
- Whether shared layout components should be extracted once the preferred route stabilises.
