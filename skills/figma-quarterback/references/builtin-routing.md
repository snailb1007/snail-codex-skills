# Built-In Figma Routing

## Intent to Skill Map

- Read Figma and understand exact design:
  `figma` plus `$figma-design-extract`
- Implement code from Figma:
  `figma:figma-implement-design` for narrow jobs
  `$figma-convert-apply` for orchestrated, multi-file, or verification-heavy jobs
- Write a page or screen into Figma:
  `figma:figma-generate-design`
  load `figma:figma-use` first for any actual file mutation workflow
- Build or update a design system in Figma:
  `figma:figma-generate-library`
  add `figma:figma-use` when the workflow will mutate the file directly
- Create Code Connect mappings:
  `figma:figma-code-connect`
- Generate project-specific design-system rules:
  `figma:figma-create-design-system-rules`

## When Quarterback Must Stay In Control

- The request starts from Figma but ends in both code and Figma.
- The user asks for a full screen or layout and the repo already has partial UI to reuse.
- The task spans multiple child components plus a composed parent surface.
- Code-connect mapping should only happen after implementation stabilizes.
- Design-system work affects both Figma and local tokens.

## Recommended Sequence For Hybrid Jobs

1. Extract once.
2. Classify reuse and split waves.
3. Implement and verify code.
4. Push or reconcile the resulting structure back into Figma if requested.
5. Add Code Connect only after component names and boundaries stop moving.
