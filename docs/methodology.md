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

### Profile-aware ranking

When you declare a `profile` (see [configuration.md](configuration.md)), radar
combines the rubric with your context. An item that touches one of your
`projects` — its stack, focus, or a dependency it relies on — is promoted, and a
direct project impact is treated as `must_see`. Items matching your `interests`
rank above items that match neither a project nor an interest. This is what
turns a generic feed into a digest about *your* work.

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

## Explain simply, then make it personal

A digest is only useful if you actually understand each item and can see why it
concerns you. Every item is written in two layers:

- **What it is** — a plain-language explanation with no jargon, written for
  someone who has never heard of the product. Unavoidable terms are glossed in a
  few words.
- **Why it matters to you** — when a profile is set, radar names the specific
  project, stack, interest, or role affected and states the concrete change for
  you, rather than a generic benefit.

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
