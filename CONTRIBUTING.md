# Contributing

Welcome, teammate! 👋 This is a fast-moving hackathon project, so the goal is
**move quickly without stepping on each other**. Here's the lightweight workflow.

## Branch & PR workflow

1. **Never commit straight to `main`.** Keep `main` always demo-able.
2. Branch off `main` with a short, descriptive name:
   ```bash
   git checkout main && git pull
   git checkout -b feat/scoreboard-ui
   ```
   Prefixes: `feat/`, `fix/`, `chore/`, `docs/`, `spike/`.
3. Commit small and often with clear messages (see below).
4. Push and open a **Pull Request** into `main`. Fill out the PR template.
5. Get a quick 👍 from a teammate if one is around — during crunch time, a
   self-merge after CI/local checks is fine. Use judgment.

## Commit messages

Keep them short and present-tense. [Conventional Commits](https://www.conventionalcommits.org/)
style is encouraged but not required:

```
feat: add live match scoreboard
fix: correct timezone on kickoff times
docs: update setup steps in README
```

## Code style

- An [`.editorconfig`](.editorconfig) keeps indentation and line endings
  consistent across machines — make sure your editor respects it
  (most do automatically, or via a plugin).
- Add a formatter/linter for your stack once it's chosen (e.g. Prettier,
  Black, gofmt) and note the command here.

## Secrets

- **Never commit secrets, API keys, or `.env` files.** They're gitignored —
  keep it that way.
- Commit a `.env.example` with blank/placeholder values so teammates know
  what variables they need.

## Need help?

Open an issue using one of the templates, or ping the team chat. When in
doubt, ship something small and iterate. 🚀
