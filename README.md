# Sonarr and Radarr for Mere Mortals

A media library rots quietly. Files land
in a downloads folder with names like
`dragnet.1951.s01e01.the.human.bomb.720p.mkv`,
nobody renames them, nobody remembers
which episodes are missing, and the
"library" becomes a pile. **Sonarr** and
**Radarr** are the pair of programs that
stop the rot. Sonarr looks after
television series; Radarr looks after
films. Each one keeps a catalogue of
what a series or film *should* contain —
every season, every episode, every
release date — compares it with the
files you actually have, and organises
those files into a tidy library with
sensible names.

Together they are nicknamed the
**\*arr stack** (the name is pronounced
"arr", like a pirate, and the family has
grown cousins — Lidarr for music,
Readarr for books, Prowlarr for indexers
— that this guide does not cover). The
two programs share most of their design:
the same web interface shape, the same
idea of a quality profile, the same way
of talking to download clients. Learn
one and the other feels familiar. This
guide teaches both side by side, and
says plainly where they differ.

One boundary is drawn early, because
everything else depends on it. Sonarr
and Radarr are **librarians, not
sources**. They track, organise, rename
and keep score. They do not host,
sell, or supply programmes or films,
and this guide uses them the way it
teaches everything else in this series:
on media the reader already owns —
recordings, home videos, and
public-domain classics — with the
download machinery explained as
mechanics, never as a route to somebody
else's property.

The lab behind this guide ran the real
thing: **Sonarr 4.0.20.3014** and
**Radarr 6.4.4.10685**, the official
Linux builds, side by side on one small
machine. Against them the lab added a
root folder to each, looked up and added
a public-domain television series
(*Dragnet*, 1951 — 9 seasons, 276
episodes) and a public-domain film
(*Night of the Living Dead*, 1968),
changed a quality profile's cutoff and
read it back, registered a SABnzbd
download client in both, and then did
the part most guides skip: it made real
video files with ffmpeg, watched both
programs refuse the fake ones, and
imported the good ones — renamed,
re-filed, and counted in the library.
What could not be run is labelled, not
faked: no indexer account and no live
download over the internet took place
in this lab, and chapter 7 says exactly
where that line falls. `criteria.md`
keeps the full ledger.

## What this guide covers

- [**What the *arr stack is**](what-the-arr-stack-is.md) —
  the mental model: a catalogue, a
  library, and a scorekeeper for each,
  what Sonarr and Radarr share, and
  where film and television genuinely
  differ
- [**The moving parts**](the-moving-parts.md) —
  series and films, root folders,
  metadata services, indexers, download
  clients, quality profiles, and the
  import pipeline — and which part holds
  what
- [**Installing Sonarr and Radarr**](installing-the-arr-stack.md) —
  the official Linux builds, the data
  folder each one keeps, the two ports,
  and the first-run checks that prove
  they are alive
- [**Your first series**](your-first-series.md) —
  a root folder, a metadata lookup, and
  a whole series catalogue added in
  minutes — plus the same shape for a
  first film in Radarr
- [**Quality profiles and cutoffs**](quality-profiles.md) —
  the ranked list of picture qualities,
  what a cutoff means, when upgrades
  stop, and the edit the lab made and
  read back
- [**Indexers and how search works**](indexers-and-search.md) —
  what an indexer is, why a fresh
  install has none, the two search
  shapes (RSS and interactive), and
  what the lab could and could not test
- [**Connecting a download client**](connecting-a-download-client.md) —
  handing finished work to SABnzbd:
  categories, priorities, the test
  button, and the connection error the
  lab met on purpose
- [**Renaming and organising the library**](renaming-and-organising.md) —
  the naming formats, season folders,
  why renaming starts switched off, and
  what an imported file is called
- [**Importing files you already have**](importing-files-you-already-have.md) —
  manual import, the sample check that
  refuses stub files, and the folder
  scan that wants one download at a time
- [**Calendars and monitoring**](calendars-and-monitoring.md) —
  air dates and release dates on a
  calendar, the missing list, and what
  the monitor switch really commits you
  to
- [**Recipes**](recipes.md) — a tidy
  starter setup, a home-video library,
  a public-domain classics shelf, and a
  weekly five-minute check
- [**The neighbours**](the-neighbours.md) —
  SABnzbd doing the downloading,
  Prowlarr feeding both apps their
  indexers, a media server playing what
  the library holds, and doing it all by
  hand
- [**Limits**](limits.md) — no content
  of their own, metadata that comes
  from outside, renaming that trusts
  the file over its name, and the rest,
  stated plainly
- [**Troubleshooting**](troubleshooting.md) —
  the folder that never appears, the
  file refused as a sample, the scan
  that imports nothing, the client that
  will not connect, and the traps this
  guide's lab fell into
- [**Glossary**](glossary.md) — the
  terms, collected in one place

## What it doesn't cover

Getting programmes or films you do not
have the right to hold — the stack is a
librarian, and this guide keeps it that
way. The cousins (Lidarr, Readarr,
Bazarr, Prowlarr) get a chapter-12
pointer, not a tutorial; Prowlarr in
particular deserves its own guide.
Running either program as a public
internet service is out of scope: these
are home tools, and chapter 12 is
honest about their security shape.
Media *playback* belongs to the media
server's guide, not this one.

## How to use this guide

Read chapter 1 for the model and
chapter 2 before installing anything —
knowing which part holds what turns
later confusion into a named problem.
Chapter 3 installs both programs;
chapter 4 adds your first series and
film in the same sitting. After that
the chapters are independent: profiles
before indexers if you automate,
renaming and importing first if your
problem is a pile of files you already
own. The lab's transcripts live in
`arr-stack-lab/transcripts/`, numbered
in the order the work was done, and
`criteria.md` maps each claim to the
transcript that backs it.

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [SABnzbd for Mere Mortals](https://paulsullivan33-dev.github.io/sabnzbd-for-mere-mortals/)
- [Backups for Mere Mortals](https://paulsullivan33-dev.github.io/backups-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/arr-stack-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/arr-stack-for-mere-mortals/blob/main/LICENSE-CODE).
