# Contributing

Thanks for considering a contribution to radar! This project aims to be a clean,
reusable Claude Code skill, so a few conventions keep it consistent.

## Ground rules

- **English only** — all files, comments, and commit messages are in English.
  The digest output language is configurable, but the project itself is not.
- **No personal data** — never include real names, emails, absolute paths,
  tokens, or private sources in code, examples, or tests. Use neutral,
  fictional examples.

## Commit messages

This project uses [Conventional Commits](https://www.conventionalcommits.org/):

```text
<type>: <short summary>
```

Common types: `feat`, `fix`, `docs`, `chore`, `ci`, `refactor`, `test`.
Example: `feat: add rss source method`.

## Versioning

Releases follow [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`.
Breaking changes bump MAJOR, new backward-compatible features bump MINOR, fixes
bump PATCH. Update `CHANGELOG.md` in the same PR as your change.

## How to add a new source method

A "method" is how radar scans a source (`webfetch`, `websearch`,
`github_trending`). To add one (e.g. `rss`):

1. Document the new `method` and its required fields in `docs/configuration.md`.
2. Add a handling branch in the Scan step of `skills/radar/SKILL.md`.
3. Add an example entry to `config/sources.example.yml`.
4. Verify a digest still generates end to end.

## Before you open a PR

- Run the project through `/radar` once to confirm it still works.
- Make sure no personal data leaked into any file.
- Fill in the pull request checklist.
