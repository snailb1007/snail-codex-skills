# Figma Quarterback Pipeline

## Default Operating Model

1. Identify the surface.
- `layout`: shell plus regions such as header, sidebar, footer, content.
- `screen`: one page inside a layout.
- `dialog` or `drawer`: overlay surface with its own open state and backdrop rules.
- `component`: isolated reusable unit.

2. Extract before building.
- Prefer `get_design_context` for implementation-grade structure.
- Use `get_metadata` only for topology or node discovery.
- Pull `get_screenshot` when the raw design context is too abstract to resolve layout intent.
- Pull `get_variable_defs` when tokens appear to exist and should override ad hoc values.

3. Produce an implementation contract.
- Exact nodes consulted.
- States and variants.
- Reuse candidates in the codebase.
- Regions and component boundaries.
- Trap list.

4. Build in waves.
- Wave 0: tokens, fonts, shared infra, story/viewports, asset plumbing.
- Wave 1: independent leaf components.
- Wave 2+: dependent composites.
- Final wave: compose the full surface.

5. Verify in the same order every time.
- Structural agreement first.
- CSS or layout metrics second.
- Visual comparison last.
- Manual Figma screenshot check only when automated verification is impossible or degraded.

## Never Skip

- Explicitly separate extraction from implementation.
- Explicitly distinguish reuse, extend, and build-new decisions.
- Explicitly name every supported state before code edits.
- Explicitly record degradations instead of silently accepting them.
