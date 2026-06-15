# myskills

This repository is a personal catalog of Codex skills that I use across projects.

Each top-level folder is one standalone skill. A skill contains the instructions,
references, scripts, and optional assets needed for Codex to perform a repeatable
task with project-specific standards.

## Repository Structure

```text
myskills/
  fp/
    SKILL.md
    agents/openai.yaml
    references/
    scripts/
```

## Skills

| Folder | Skill | Purpose |
|---|---|---|
| `fp/` | Korea FP Guide Validation | Validate Function Point workbooks and FP function lists against the Republic of Korea SW project cost estimation guide. |

## Skill Folder Convention

Each skill folder should follow this structure when applicable:

```text
<skill-name>/
  SKILL.md                 # Required skill instructions and trigger description
  agents/openai.yaml       # Optional UI metadata
  references/              # Optional detailed rules and reference material
  scripts/                 # Optional executable helpers
  assets/                  # Optional templates or reusable assets
```

## Adding a New Skill

1. Create a new top-level folder using a short lowercase name.
2. Add a valid `SKILL.md` with clear YAML frontmatter:

   ```yaml
   ---
   name: skill-name
   description: What the skill does and when Codex should use it.
   ---
   ```

3. Put detailed standards in `references/` when they are too long for `SKILL.md`.
4. Put repeatable deterministic utilities in `scripts/`.
5. Validate the skill before committing:

   ```bash
   python3 ~/.codex/skills/.system/skill-creator/scripts/quick_validate.py <skill-folder>
   ```

6. Commit each skill or meaningful update separately.

## Local Installation

To use a skill locally, copy or sync the skill folder into Codex's skills directory:

```bash
mkdir -p ~/.codex/skills
rsync -a fp/ ~/.codex/skills/korea-fp-guide-validation/
```

After installing, restart or reload Codex if the current session does not discover the skill.

## Notes

- Keep skills self-contained and reusable.
- Do not store project-private data, source workbooks, credentials, or generated reports in this repository.
- Prefer concise `SKILL.md` files and move detailed domain rules into `references/`.
- Scripts should be safe to run on user-provided inputs without overwriting originals.
