# Configuration

radar reads two YAML files from your project's `config/` directory:

- `config/sources.yml` — the sources to scan (copy from `sources.example.yml`)
- `config/radar.config.yml` — output, language and scoring settings (copy from `radar.config.yml.example`)

Both are **gitignored**: your personal configuration never leaves your machine.

## Config resolution order

radar resolves each setting in this order (first match wins):

1. An explicit argument passed to the skill
2. Your project config (`config/sources.yml`, `config/radar.config.yml`)
3. The shipped defaults (resolved from the skill's own location, **not** the
   current working directory — so the skill works the same whatever folder you
   run it from)

## `sources.yml`

A single `sources` list. Each entry is one source, typed by its `method`.

| Field | Required | Allowed values | Default | Notes |
|-------|----------|----------------|---------|-------|
| `name` | Yes | string | — | Human-readable label shown in the digest |
| `method` | Yes | `webfetch` \| `websearch` \| `github_trending` | — | How the source is scanned |
| `url` | Conditional | string (URL) | — | Required for `webfetch` and `github_trending` |
| `query` | Conditional | string | — | Required when `method: websearch` |
| `priority` | No | `high` \| `medium` \| `low` | `medium` | Hints how strongly to weigh the source |
| `tags` | No | list of strings | `[]` | Free-form labels, surfaced in the digest |

### Methods

- **`webfetch`** — fetch and read a specific page (`url` required).
- **`websearch`** — run a web search (`query` required).
- **`github_trending`** — scan a GitHub trending page (`url` required, e.g.
  `https://github.com/trending?since=daily`).

## `radar.config.yml`

| Field | Required | Type | Default | Notes |
|-------|----------|------|---------|-------|
| `output_dir` | No | string (path) | `./digests` | Where digests are written. Must stay inside the project folder |
| `index_file` | No | string (path) | `./digests/index.md` | Dedup index, generated and gitignored |
| `language` | No | string | `en` | Digest output language (`en`, `fr`, ...) |
| `max_items` | No | integer | `10` | Maximum items per digest |
| `profile` | No | map | none (generic mode) | Your adaptive context — drives personalized ranking and explanations |
| `scoring` | No | map | shipped defaults | Rubric strings: `must_see`, `interesting`, `bonus` |
| `categories` | No | list of strings | shipped defaults | Digest section names, rename for your domain |

### `profile` — the adaptive context

`profile` is what makes a digest *yours*. When set, radar uses it both to
**rank** items (anything touching your projects or interests rises to the top)
and to **explain** them (each item gets a "Why it matters to you" that names the
specific project, stack, interest, or role it affects). Leave `profile` out and
radar runs in generic mode: plain explanations and a general benefit, with no
personalization.

| Sub-field | Required | Type | Notes |
|-----------|----------|------|-------|
| `role` | No | string | One line on who you are. Shapes tone and what counts as "actionable" |
| `interests` | No | list of strings | Topics you follow. Used to rank and to phrase relevance |
| `projects` | No | list of maps | Your projects. Each item is mapped to these by name |
| `projects[].name` | No | string | Project name, quoted back to you in "Why it matters to you" |
| `projects[].stack` | No | string | Tech/stack, so radar can match a tool or release to it |
| `projects[].focus` | No | string | What the project does, to judge real impact |

## What happens if a field is missing or wrong

radar is **fail-loud**: it tells you exactly what to fix instead of producing a
silent, partial digest.

- **`sources.yml` missing** — radar stops and tells you to copy
  `config/sources.example.yml` to `config/sources.yml`.
- **Unknown `method`** — radar warns, skips that one source, and continues.
  The skipped source is always listed in the run output.
- **Missing required field** (e.g. `query` for a `websearch` source) — radar
  reports which source and which field, then skips that source.
- **Invalid YAML** — radar tells you to check the indentation (YAML is
  whitespace-sensitive) and stops.
- **`output_dir` outside the project folder** — radar refuses to write there,
  for safety.

A run never produces a partial digest without listing what was skipped.
