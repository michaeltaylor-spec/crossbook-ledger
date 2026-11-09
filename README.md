# Crossbook ledger

Every forecast Crossbook has published, one JSON object per line, in
`data/ledger.jsonl`.

## Why this repo exists

Crossbook publishes probability estimates on prediction markets and scores them
in public. Every date on crossbook.tech is a date Crossbook wrote, on a page
Crossbook serves, out of a database Crossbook controls. That is worth nothing to
a reader who has no reason to trust the site — which is the only reader a track
record is for.

This repo is the part Crossbook cannot rewrite. The commit timestamps are
GitHub's. A forecast committed here before an event resolved cannot be edited
afterwards without the edit itself being a commit.

## Read this before you trust the dates

**The first commit is a batch import and is labelled `backfill: initial ledger
import`.** Everything in it was published on crossbook.tech before this repo
existed, and the `published_at` field in those lines is the date the site
recorded — not the date it was committed here. Those entries are corroborated by
the site and by nothing else.

**Every commit after that one was made at the moment of publication.** Those are
the entries where the GitHub timestamp is independent evidence.

If that distinction were not stated, a careful reader would have to assume the
whole file was written in one sitting, which would make the repo pointless. It
is stated so the commits above the boundary mean something.

## The format

One JSON object per line. Append-only: a commit that modifies an existing line
is a bug, and because each entry is its own line, every ordinary commit shows
exactly one added line and no removed ones. That is checkable by eye in any
diff view, which is the reason the file is not a JSON array.

```
public_id     the permanent id, also the anchor at crossbook.tech/record#t-0142
market        the question, as the venue worded it
venue         polymarket or kalshi
p_crossbook   Crossbook's probability, 0-1
p_market      the venue's price at the moment the forecast was made, 0-1
published_at  when the forecast was committed on the site
thesis        the reasoning, as published
falsifier     what would show the forecast was wrong
```

Nothing appears here that is not already public at
[crossbook.tech/record](https://crossbook.tech/record), with one stated
exception below.

## The `c-` entries

Entries whose `public_id` starts with `c-` (c-0001 onward, first committed
November 8, 2026) are a separate test, not the main Crossbook forecaster. They
are logged here first and may appear on crossbook.tech later or not at all.

- They are made by Claude agents, not the pipeline that produces the `t-`
  entries. `generation_method` is `claude-agent-price-blind`.
- One agent gathers sourced facts with every prediction-market and betting price
  removed. A second agent forecasts from those facts alone and never sees a
  market price. The market price is pulled only afterwards, to decide whether
  the disagreement clears the 3-point floor.
- They are not blended with the market price (`blend_share` is 0), unlike
  recent `t-` entries.
- They should be scored as their own group, not pooled into the main record.

Each was committed before its event resolved, so the GitHub timestamp is
independent evidence for these entries too.

## What this repo is not

It is not the scored record. Outcomes, Brier scores and resolutions live on the
site, because they change as markets settle and this file does not. This is the
evidence that a forecast existed and said what it says, at a time Crossbook
could not have chosen.

## Late and held entries

**Late entries.** 70 forecasts published on crossbook.tech between
1 September 2026 and 2 November 2026 were not committed here when they were published: the site
started the commit after responding, and its server often stopped before the
commit finished. They were added afterwards in a commit whose message begins
`late:`. For those lines the GitHub timestamp proves nothing; `published_at`
is the site's own date. Any commit beginning `late:` means the same thing. The
site now checks every hour that each published call is here.

**Held entries.** t-0192, t-0193, t-0199, t-0203, t-0204, t-0206, t-0207, t-0210, t-0224, t-0227 are forecasts Crossbook made
but held back because each was further from the market price than its
category's limit allows. A bug committed them here anyway. They are not on
crossbook.tech's public record and are not scored. They stay in this file
because it is append-only: removing lines is the edit this repo exists to rule
out.
