# Somantra Skills Repository

This repository is set up around the `somantra-project-analyst` skill for publishing to [skills.sh](https://skills.sh/).

## Repository Layout

Each skill lives in its own folder under `skills/`:

```text
skills/
  <skill-name>/
    SKILL.md          # required
    scripts/          # optional
    references/       # optional
    assets/           # optional
```

## Current Skill

- `skills/somantra-project-analyst`

## Publishing Checklist

1. Keep the skill in `skills/somantra-project-analyst`.
2. Ensure `SKILL.md` has YAML frontmatter with:
   - `name` (must match folder name)
   - `description` (clear what + when to use)
3. Keep or update `somantra-project-analyst.skill` as the packaged artifact.
4. Push this repository to GitHub.
5. Import the GitHub repo in [skills.sh](https://skills.sh/) and publish.

## Notes

- Keep `name` lowercase with letters, numbers, and hyphens.
- Keep descriptions specific and keyword-rich for discovery.
- Add supporting files in `scripts/`, `references/`, or `assets/` only when needed.
