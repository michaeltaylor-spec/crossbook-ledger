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
[crossbook.tech/record](https://crossbook.tech/record).

## What this repo is not

It is not the scored record. Outcomes, Brier scores and resolutions live on the
site, because they change as markets settle and this file does not. This is the
evidence that a forecast existed and said what it says, at a time Crossbook
could not have chosen.
