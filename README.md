# Codex Global Skills Export

Repository nay la ban tach cac global skills tu `~/.codex/skills` de dua len GitHub thanh project rieng.

## Scope

- Da export toan bo thu muc top-level trong `~/.codex/skills`
- Co chu y bo qua `.system`
- Co chu y bo qua `codex-primary-runtime`

## Layout

- `skills/`: moi skill duoc giu nguyen thanh mot thu muc rieng

## Refresh From Global

Neu muon dong bo lai tu may local:

```bash
rsync -a --exclude '.system' --exclude 'codex-primary-runtime' ~/.codex/skills/ ./skills/
```

## Next Steps

```bash
git remote add origin <your-repo-url>
git add .
git commit -m "Initial export of global Codex skills"
git push -u origin main
```
