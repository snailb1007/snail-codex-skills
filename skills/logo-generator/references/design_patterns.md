# Logo Design Patterns

Use this file when generating logo variants from scratch. It defines the design rules and pattern families to diversify concepts without drifting into random ornament.

## Core rules

- Keep 1-2 core elements maximum.
- Leave at least 40% negative space.
- Use stroke widths around 2.5-4 in a `0 0 100 100` viewBox.
- Create one focal point.
- Prefer restrained geometry over effects.
- Use asymmetry intentionally when it adds tension.
- Ensure structural stability at small sizes.
- Round negative-space cutouts instead of using sharp cuts.

## Pattern families

### Pure geometry

Use circles, arcs, polygons, ring systems, or one strong closed form for brands that need authority, precision, or memorability.

Good for:
- Infrastructure
- Security
- Hardware
- Minimalist brands

### Dot matrix

Use circles, rounded rectangles, capsules, or hexagon cells to suggest data, modularity, or digital systems.

Good for:
- AI
- Analytics
- Developer tools
- Modular platforms

### Line systems

Use waves, parallel line fills, spirals, or directional strokes for brands about flow, signals, or transformation.

Good for:
- Communication
- Audio
- Workflow tools
- Motion-driven products

### Node networks

Use node-edge compositions to represent connections, agents, graph structures, or collaboration systems.

Good for:
- Agent frameworks
- Social or graph products
- Integration platforms

### Mixed compositions

Combine two pattern families when the concept benefits from both structure and texture:

- dots + geometry
- lines + geometry
- nodes + geometry
- subtle background pattern + bold foreground symbol

## Variant allocation

When generating 6+ variants, distribute them deliberately:

1. Pure geometric
2. Dot matrix
3. Line system
4. Mixed dots + geometry
5. Mixed lines + geometry
6. Node network or layered composition

Vary:
- Density
- Symmetry
- Weight
- Complexity

## SVG best practices

- Use `currentColor`.
- Group related elements with `<g>`.
- Use `<defs>` and `<use>` for repeated shapes.
- Leave 10-15 units of padding from the edge.
- Keep the logo legible at favicon size.

## Quality check

Before presenting a variant, confirm:

- It is visually distinct from the other variants.
- It works at 16x16 and 512x512.
- The rationale connects to the product concept.
- The composition still reads clearly without labels.
