# The Moving Parts

**Outcome:** you can name each part of the system, say which
program owns it, and predict where a problem lives when
something goes wrong.

**Check:** for each part below, say whether it lives inside
Sonarr/Radarr, in another program, or on the internet — from
memory, before you re-read.

## The catalogue entry: series and films

Everything starts with an entry in the catalogue. A
**series** in Sonarr holds its title, its TVDB id, its
network and status, and a list of seasons, each holding
episodes with titles and air dates. A **movie** in Radarr
holds its title, year, TMDB and IMDb ids, and its three
release dates.

Neither program invents this data. When you search for
something to add, the program asks an outside **metadata
service** — Sonarr asks its **SkyHook** proxy, which serves
TheTVDB's data; Radarr asks a proxy of TMDB's data — and
shows you the candidates. The lab typed `Dragnet` and got
four candidates back, including *Dragnet (1951)*, TVDB id
72763 (transcript t03). Posters and fan art are then fetched
from those services' image servers, which is why a freshly
added entry dresses itself up over the following minute.

The catalogue is the program's memory of the world. Files
come later, and are judged against it.

## The root folder

A **root folder** is a directory the program is allowed to
file media into — one for series in Sonarr, one for films in
Radarr, or several if your disks demand it. Adding one is a
single API call or two clicks, and the program reports the
free space on that filesystem when you do (transcript t02).

Each entry gets its own folder under the root: adding
*Dragnet (1951)* reserved the path
`…/media/tv/Dragnet (1951)` whether or not any file existed
yet. Whether the folder is *created* immediately is a
setting — as installed, `createEmptySeriesFolders` is off in
Sonarr, so the folder arrives with the first imported file
(transcript t05). Knowing that saves a confused half hour;
chapter 13 returns to it.

## Quality profiles

A **quality profile** is a ranked list of picture qualities
— SDTV at the bottom, through HDTV and WEBDL at 720p and
1080p, up to Bluray and remux at the top — with three
decisions baked in:

- which qualities are **allowed** at all,
- a **cutoff**: the quality at which the program stops
  wanting better, and
- whether **upgrades** are allowed below that cutoff.

Both programs install with the same six starter profiles
(Any, SD, HD-720p, HD-1080p, Ultra-HD, HD - 720p/1080p).
Chapter 5 takes them apart; transcript t18 prints the full
HD-1080p table from both programs, including Radarr's
film-only rows (CAM, TELESYNC, WORKPRINT) that Sonarr does
not have.

## Indexers

An **indexer** is a searchable catalogue of *releases* —
posts and files that exist out in the world, described by
name, size and quality. Sonarr and Radarr do not ship with
any: a fresh install's indexer list is empty in both
(transcript t08), because an indexer is an outside service
you choose and usually hold an account with. What the
programs ship with is the ability to *speak* to indexers —
the schema list includes **Newznab** and **Torznab**, the
two dialect standards, plus a handful of built-in site
types.

Chapter 7 covers how searching works. For now, hold the
shape: the catalogue says what *should* exist, indexers say
what *does* exist, and a search is the program matching the
two against a quality profile.

## Download clients

When the program decides a release is worth having, it does
not fetch it. It hands the job to a **download client** —
SABnzbd for Usenet downloads, or one of the torrent clients
— with a category attached ("tv", "movies"), and watches
the client's queue. The client is a separate program with
its own guide in this series; chapter 8 registers one in
both apps and shows what the handshake looks like, including
its failure mode.

## The import pipeline

The last part is the one this guide's lab exercised hardest.
When a download finishes — or when you point the program at
files you already have — the **import pipeline**:

1. **parses** each file's name for series, season, episode
   (or film and year) and a claimed quality,
2. **checks** the file itself: is it really video, how long
   is it, what resolution does it actually carry,
3. **decides**: matched against the catalogue, checked
   against the profile, refused with a stated reason if it
   fails (a too-short file is refused as a *sample* — the
   lab met this twice, transcripts t10–t11),
4. **moves or copies** the file into the library folder,
   **renaming** it on the way if renaming is on, and
5. **records** the event in history, so the scorecard —
   episodes on disk, films with files — is never a guess.

Chapter 10 walks the pipeline with real files, including
its two failure modes and the fix for each.

## The API underneath

Every part above is reachable through the program's **API**,
protected by an **API key** the program generates on first
run and stores in its `config.xml`. The lab drove everything
in this guide with `curl` and that key, and the transcripts
are those calls. You never need the API — the web interface
does the same things — but knowing it exists explains the
programs' honesty: a setting you can read back is a setting
you can check, and every chapter here ends with such a
check.
