# Installation

## Quick start (3 commands)

```text
/plugin marketplace add Samdev2420/radar-ai
/plugin install radar
/radar
```

That's it — the third command runs your first digest once you've declared your
sources (see below).

## Method 1 — Install as a Claude Code plugin (recommended)

1. Add the marketplace:
   ```text
   /plugin marketplace add Samdev2420/radar-ai
   ```
2. Install the plugin:
   ```text
   /plugin install radar
   ```

This installs the `radar` skill and makes `/radar` available in any project.

## Method 2 — Manual install

1. Clone the repository:
   ```bash
   git clone https://github.com/Samdev2420/radar-ai.git
   ```
2. Copy the skill into your Claude Code skills directory:
   ```bash
   cp -r radar-ai/skills/radar ~/.claude/skills/radar
   ```

## Configure your sources

radar ships with example configuration. Copy each example to its real name
(the real files are gitignored, so your settings stay private):

```bash
cp config/sources.example.yml      config/sources.yml
cp config/radar.config.yml.example config/radar.config.yml
```

Then edit `config/sources.yml` to declare the sources you want to watch, and
`config/radar.config.yml` to set the output folder, language, and scoring.
See [configuration.md](configuration.md) for the full field reference.

## Run it

```text
/radar
```

radar scans your sources, deduplicates against the index, scores and
categorizes the items, and writes the digest to your `output_dir`
(default: `./digests/`). The dedup index lives at `./digests/index.md` so the
same item never shows up twice.
