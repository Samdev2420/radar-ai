# Security Policy

## Supported versions

| Version | Supported |
|---------|-----------|
| 1.0.x   | Yes       |

## Reporting a vulnerability

Please report security issues privately through GitHub's **private
vulnerability reporting** on this repository:

1. Go to the repository's **Security** tab.
2. Click **Report a vulnerability**.
3. Describe the issue and, if possible, steps to reproduce.

Please do not open a public issue for security reports.

## Threat model

radar is a Claude Code skill that reads local config, scans declared sources,
and writes Markdown digests. Its security posture rests on two guarantees:

- **Confined writes** — radar writes only inside the validated `output_dir` /
  `index_file`, and refuses any path resolving outside the project folder. It
  never runs destructive commands.
- **Prompt-injection resistance** — content fetched from the web is treated as
  untrusted data, never as instructions. radar ignores any directive embedded
  in a fetched page, search result, or repository, and only acts on the user's
  config and this skill.

## Protect your own data

Your real configuration is gitignored on purpose. **Never commit your
`config/sources.yml` or `config/radar.config.yml`**, and never put secrets,
tokens, or personal paths in the example files. Only the `*.example` files are
tracked.
