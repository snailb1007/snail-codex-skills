---
name: logo-generator
description: Generate professional SVG logos, logo concept sets, and polished showcase assets for brands or products. Use when Codex needs to: create a new logo or icon from product/brand context, explore multiple logo directions, iterate on an existing logo direction, export SVG logos to PNG, or produce high-end logo presentation imagery and showcase pages from a chosen logo.
---

# Logo Generator

Generate logo concepts, SVG mark variants, PNG exports, and showcase assets.

Keep the working loop narrow: gather only the product cues needed to design, produce several meaningfully distinct SVG directions, refine the short list, then export and present the chosen direction.

## Workflow

### 1. Gather design inputs

Ask only for the missing essentials:

- Product or brand name
- Industry or category
- Core idea to express
- Style direction: minimal or expressive, geometric or organic
- Color preference: monochrome or directed palette
- Mood: cold, warm, premium, playful, technical, editorial

If the user already gave enough context, do not re-ask it.

### 2. Generate distinct logo directions

Create at least 6 genuinely different variants. Avoid producing parameter tweaks that look like the same logo.

Use [references/design_patterns.md](references/design_patterns.md) to select pattern families and composition rules. Keep these constraints:

- Use `viewBox="0 0 100 100"` in SVG
- Use `currentColor` for fills and strokes
- Preserve generous negative space
- Keep one clear focal point
- Prefer simple, scalable geometry over decorative complexity

For each variant, provide:

- A short title
- A one-line rationale tied to the brand concept
- The SVG markup
- Optional notes on where it works best: app icon, favicon, hero mark, print, etc.

### 3. Build a comparison showcase

Use [assets/showcase_template.html](assets/showcase_template.html) as the starting point when the user wants a comparison page for multiple concepts. Populate it with:

- Product name
- Variant titles and rationales
- Inline or referenced SVG variants
- Optional final showcase section once rendered imagery exists

Keep the page readable and comparison-oriented rather than overdesigned.

### 4. Refine instead of restarting

When the user picks 1-3 directions, make targeted edits:

- Adjust spacing, stroke weight, symmetry, or cutouts
- Merge successful traits from two variants if requested
- Change color treatment without rebuilding geometry
- Produce 2-4 focused follow-up variants around the preferred direction

Do not regenerate the full exploration unless the user asks.

### 5. Export raster assets

Use `scripts/svg_to_png.py` to convert a selected SVG to PNG:

```bash
python3 scripts/svg_to_png.py path/to/logo.svg --output path/to/logo.png --width 1024 --height 1024
```

Use transparent backgrounds unless the user asks otherwise.

### 6. Generate presentation imagery

When the user wants high-end mockups or presentation renders:

1. Convert the chosen SVG to PNG.
2. Read [references/background_styles.md](references/background_styles.md) and recommend 3-4 fitting styles.
3. If the user wants dynamic WebGL background directions, use [references/webgl_backgrounds.md](references/webgl_backgrounds.md) and [assets/background_library.html](assets/background_library.html).
4. Use `scripts/generate_showcase.py` to render showcase images from the PNG reference.

Example:

```bash
python3 scripts/generate_showcase.py "BrandName" path/to/logo.png --style iridescent --description "AI productivity platform"
```

To generate all available styles:

```bash
python3 scripts/generate_showcase.py "BrandName" path/to/logo.png --all-styles --description "AI productivity platform"
```

## References

- Read `references/design_patterns.md` before generating concepts from scratch.
- Read `references/background_styles.md` when choosing polished static showcase styles.
- Read `references/webgl_backgrounds.md` when the user wants interactive or shader-driven presentation directions.

## Scripts

- `scripts/svg_to_png.py`: Convert SVG files to PNG using CairoSVG.
- `scripts/generate_showcase.py`: Generate showcase images from a PNG logo reference using Gemini-compatible image APIs.

Install script dependencies from `requirements.txt`. Copy `.env.example` to `.env` and set `GEMINI_API_KEY` before using showcase generation.

## Delivery

When the task is complete, return only the assets the user asked for:

- SVG variants
- Refined finalists
- PNG exports
- Showcase images
- Comparison or presentation HTML

Explain briefly why the chosen directions fit the brand. Keep critique concrete and visual.
