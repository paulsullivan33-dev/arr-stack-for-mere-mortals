# Indexers and How Search Works

**Outcome:** you understand what an indexer contributes,
why your fresh install has none, and the difference between
the two ways the programs search — including which parts of
this chapter the lab could verify and which it could not.

**Check:** the indexer list call below answers `[]` on a
fresh install in both programs, and the schema call lists
the indexer *types* each program can speak to.

## What an indexer is

An **indexer** is a catalogue of releases that exist out in
the world — for Usenet, a searchable index of posts; for
torrents, a tracker or listing site. Where the metadata
service (chapter 4) knows what *should* exist, an indexer
knows what *does* exist, described by release name, size,
age and claimed quality.

Sonarr and Radarr are not indexers and do not include one.
They are *clients* of indexers:

```bash
curl -s -H "X-Api-Key: $SONARR_KEY" http://localhost:8989/api/v3/indexer
```

```
[]
```

Empty in Radarr too (transcript t08). What the programs do
ship is fluency — the list of indexer types they can talk
to, from the schema call in the same transcript:

```
Newznab          -> the standard dialect for Usenet indexers
Torznab          -> the same idea for torrent sites
Torrent RSS Feed -> a plain feed, matched by name
…plus a handful of built-in definitions for specific sites
```

**Newznab** is the one that matters for this series:
SABnzbd's guide covers the downloading half, and a Newznab
indexer is the catalogue half — you register it with the
address and API key of an indexer service you hold an
account with (Settings → Indexers → +), and from then on
the program can ask it questions.

## The two searches

With at least one indexer registered, searching comes in
two shapes:

- **RSS search** — the background habit. Every so often
  (a quarter of an hour is typical) the program reads each
  indexer's feed of *recent* releases and compares them
  against everything monitored and missing. This is how a
  newly posted episode of a continuing series gets noticed
  without anyone pressing a button.
- **Interactive and automatic search** — the deliberate act.
  Open an episode or film and press search, and the program
  asks every indexer at once, ranks the answers against the
  quality profile — allowed qualities only, best first,
  with reasons shown for anything rejected — and either
  shows you the list (interactive) or takes the winner
  (automatic).

Both shapes end at the same gate: chapter 2's profile.
An indexer can offer a hundred releases; the profile
decides which three were ever candidates.

## What the lab verified, and what it did not

Verified live: the empty indexer list on a fresh install in
both programs, and the schema of indexer types each can
configure (transcript t08). The search *machinery* —
parsing release names into series, season, episode and
quality, and judging them — is the same machinery the lab
exercised thoroughly in chapter 10's imports, where its
decisions and rejection reasons are on record.

Not run, and labelled accordingly: registering a real
indexer (the lab holds no indexer account, and a fake one
would only test the error message), an RSS sync against a
live feed, and any search that ends in a real download.
Those flows are described here from the projects'
documentation. If you follow this guide with your own
indexer account, the setup check is the **Test** button on
the indexer form: it makes the program introduce itself to
the indexer and report back before you save — use it, and
believe it over any tutorial, this one included.

## A word on choosing indexers

An indexer is a third-party service with its own terms,
its own account, and its own key — which, like the API keys
in chapter 3, you should treat as a password. This guide
names none and ranks none. What the *stack* asks of an
indexer is narrow and practical: that it speaks Newznab or
Torznab, that its release names are parseable, and that it
is up when the RSS habit comes calling.
