# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-05-31

### Added

- `radar` Claude Code skill: scans a declarative list of sources and produces a
  deduplicated, scored Markdown tech-watch digest.
- Config-driven, multi-domain engine with no hardcoded paths.
- Adaptive `profile` (role, interests, projects): personalizes ranking and
  writes a plain-language "What it is" plus a "Why it matters to you" that names
  the specific project, stack, or interest each item affects.
- Declarative sources config (`config/sources.example.yml`): a single `sources`
  list typed by `method` (`webfetch`, `websearch`, `github_trending`).
- Digest settings config (`config/radar.config.yml.example`): `output_dir`,
  `index_file`, `language`, `max_items`, `scoring`, `categories`.
- Fail-loud config validation and confined writes (output stays inside the
  project folder).
- Prompt-injection guard: fetched web content is treated as untrusted data.
- Claude Code plugin manifest (`.claude-plugin/`) for one-command install.
- Generic digest template and an anonymized example digest.
- Documentation: installation guide, configuration contract, and methodology.
- Project governance: MIT license, security policy (GitHub private vulnerability
  reporting), contributing guide (Conventional Commits, SemVer), and a
  Contributor Covenant 2.1 code of conduct.
- GitHub issue and pull request templates.
- CI: Markdown/YAML linting and gitleaks secret scanning.

[1.0.0]: https://github.com/Samdev2420/radar-ai/releases/tag/v1.0.0
