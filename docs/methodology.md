# Methodology

radar is opinionated about one thing: a tech-watch digest is only useful if it
is **short, scored, and actionable**. This page explains how it gets there.

## Scoring

Every item that survives deduplication is scored against a rubric you control
in `radar.config.yml`. The shipped defaults are:

- **must_see** — direct impact on one of your projects, a breaking change, or a
  major new model/feature. These go to the top, with a warning if critical.
- **interesting** — relevant to your domain, but no immediate action needed.
- **bonus** — nice-to-know, enriching context.

The rubric is plain text, so you can rewrite it for any domain. radar applies
your wording when deciding what to keep and how to rank it. `priority` on each
source acts as an additional weighting hint.

## Categorization

Items are grouped under the `categories` you declare in config. Defaults are
AI/dev oriented, but renaming them is the main lever to repurpose radar for a
different field (crypto, biotech, design, ...). The engine assumes nothing
about your domain.

## Deduplication (double filter)

radar keeps a permanent index of everything it has already published
(`index_file`). On each run it filters new items twice:

1. By **canonical URL** — the strongest signal that an item was already seen.
2. By **normalized title** — a fallback for the same story published at a
   different URL.

This is why the same announcement never appears across two days, even if a
source re-lists it.

## Quality over quantity

radar caps each digest at `max_items` and prefers fewer strong items to a long
mediocre list. On a quiet day it produces a minimal "nothing to report"
digest rather than padding with filler. The goal is a digest you actually read
in full, every day.

## Fail-loud, never silent

If configuration is missing or a source can't be scanned, radar tells you
exactly what happened and what to fix — and always lists what it skipped. It
never hands you a partial digest that looks complete. See
[configuration.md](configuration.md) for the full behavior.
