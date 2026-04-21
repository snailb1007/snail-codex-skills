# Codex Global Skills

This repository is an exported collection of global skills extracted from the `~/.codex/skills` directory, designed to be version-controlled and shared as a standalone project.

## Scope

- Contains all top-level directories previously located inside `~/.codex/skills`.
- System directories like `.system` are deliberately excluded.
- The `codex-primary-runtime` component is deliberately excluded.

## Layout

- `skills/`: Every individual skill is maintained in its own dedicated subdirectory.

## Refresh From Global Source

If you need to sync updates from your local Codex installation to this repository, run the following command from the root of this project:

```bash
rsync -a --exclude '.system' --exclude 'codex-primary-runtime' ~/.codex/skills/ ./skills/
```
