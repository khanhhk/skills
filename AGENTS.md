# Repository Guidelines

## Project Structure & Module Organization
This repository stores reusable agent skills, not application source code. The main overview lives in `README.md`. Tracked skills are mirrored under `.agents/skills/<skill>/` and `.codex/skills/<skill>/`; each skill should keep the same structure across both trees:

- `SKILL.md` for workflow and rules
- `PROMPT_TEMPLATE.md` for reusable prompting patterns
- `templates/` for shipped assets such as `templates/main.tex`

Use `papers/` for reference PDFs that help validate paper-related skills. If a local `.claude/` mirror exists in your worktree, treat it as environment-specific unless it is explicitly tracked in your branch.

## Build, Test, and Development Commands
There is no build system or automated test runner yet. Use lightweight checks before opening a PR:

- `git status --short` to review pending edits
- `diff -ru .agents/skills/<skill> .codex/skills/<skill>` to confirm mirrored files stay aligned
- `find .agents .codex -maxdepth 4 -type f | sort` to verify expected files are present

When editing skill content, also read the rendered Markdown directly to catch broken headings, lists, or code fences.

## Coding Style & Naming Conventions
Use clear Markdown with short sections, imperative instructions, and concrete examples. Keep skill directory names in `kebab-case` such as `paper-to-latex-report`. Preserve required filenames exactly: `SKILL.md`, `PROMPT_TEMPLATE.md`, and template asset names already referenced by the skill. Prefer ASCII for filenames and commands; Vietnamese content is fine when it is part of the skill itself.

## Testing Guidelines
No coverage threshold is defined. For prompt or template changes, perform a manual smoke test with a sample file from `papers/` and confirm the workflow still produces the expected multi-file LaTeX structure. Review mirrored diffs together so logic does not drift between agent environments.

## Commit & Pull Request Guidelines
Current history uses short, imperative commit subjects such as `add papers` and `update skill & prompt template`. Keep commits focused and similarly concise. PRs should state which skill changed, which mirrored paths were updated, what manual validation you ran, and include sample output or template diffs when behavior changes.
