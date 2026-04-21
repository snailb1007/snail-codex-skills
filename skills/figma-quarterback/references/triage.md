# Triage Rules

## Reuse Categories

- `exists`: component already matches closely; adjust props or stories only.
- `extend`: existing component is the right base but needs new state, slot, or prop shape.
- `duplicate`: design seems new but actually maps to an existing component with different content.
- `simple`: new leaf component with shallow dependencies.
- `complex`: new component with nested states, asset handling, or downstream reuse.
- `composite`: shell or assembled surface built from lower-level parts.

## Split Heuristics

Split into separate tasks when any of these are true:
- Different states need different layout structure, not just different copy.
- The node is reused across more than one parent surface.
- Raster or vector asset handling differs by state.
- Mobile and desktop structure diverge materially.
- The surface contains a shell plus children that can verify independently.

Keep together when:
- Differences are only props, copy, or cosmetic emphasis.
- One baseline intentionally covers the shared component under a parent composite.
- Splitting would create a fake abstraction with no reuse value.

## Escalate Before Coding

- Missing fonts or asset URLs likely invalidate visual comparison.
- Parent or sibling nodes are required to understand the target node correctly.
- A mobile node is the only concrete instance of a component that will also exist on desktop.
- The extracted surface depends on design-system tokens that do not exist locally yet.
