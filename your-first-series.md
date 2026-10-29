# Your First Series

**Outcome:** Sonarr holds a whole series catalogue — every
season and episode — Radarr holds a film, and you have read
both back through the API to prove they are really there.

**Check:** the read-back at the end prints the series with
its episode count (276 for the lab's choice) and the film
with `hasFile: False` — catalogued, not yet on disk.

## Step one: a root folder

Nothing can be filed until the program knows where filing
happens. In Sonarr: **Settings → Media Management → Add Root
Folder**. In Radarr the same screen exists under the same
name. Pick (or create) the folder your media lives in — one
for television, one for films:

```
/srv/media/tv
/srv/media/movies
```

The lab added its two folders through the API (transcript
t02):

```bash
curl -s -X POST -H "X-Api-Key: $SONARR_KEY" -H "Content-Type: application/json" \
  -d '{"path": "/srv/media/tv"}' http://localhost:8989/api/v3/rootfolder
```

```json
{
    "path": "/srv/media/tv",
    "accessible": true,
    "freeSpace": 190765744128,
    "unmappedFolders": [],
    "id": 1
}
```

`accessible: true` and a real free-space figure are the
signs of a healthy answer. A path the program cannot write
to fails here, at setup time, instead of later at import
time — which is the point of doing it first.

## Step two: look something up

In Sonarr: **Add New**, and type a name. The program is not
searching your disk; it is asking its metadata service what
exists in the world. The lab typed `Dragnet` and was offered
four series (transcript t03):

```
Dragnet          | tvdbId: 77570  | year: 1967 | network: NBC
The Dragnet      | tvdbId: 415392 | year: 2021 | network: iQIYI
Dragnet (1989)   | tvdbId: 74467  | year: 1989
Dragnet (1951)   | tvdbId: 72763  | year: 1951 | network: NBC
```

Pick by the identifiers, not by the title alone — titles
repeat across decades, the **TVDB id** does not. In Radarr
the same screen asks the film service, and the stable
identifiers are the **TMDB id** and, shown alongside it, the
IMDb id:

```
Night of the Living Dead | tmdbId: 10331 | year: 1968 | status: released
Night of the Living Dead | tmdbId: 19185 | year: 1990 | status: released
```

Two films, one title, different ids — the 1968 original is
the one this guide wants, and the id is how you know you
have it.

## Step three: add, without fetching anything

Adding an entry asks for four decisions:

- **Root folder** — where its files will live.
- **Quality profile** — chapter 5; the HD-1080p starter
  profile is a sane default.
- **Monitored** — whether the program should care about the
  gap between catalogue and disk. Leave it on for now;
  chapter 11 explains what it commits you to.
- **Search on add** — whether to immediately go looking for
  files. **Untick it.** Adding is bookkeeping; searching is
  a separate act, and keeping them separate is what makes
  the system understandable. The lab added everything with
  searching off.

The lab's two additions, and their answers (transcripts
t04–t05):

```
id: 1 | title: Dragnet (1951) | monitored: True | seasons: 9 | profile: 4
id: 1 | title: Night of the Living Dead | year: 1968 | monitored: True | profile: 4 | hasFile: False
```

Within a minute or so, both entries grow posters and
background art, fetched from the metadata services' image
servers — visible proof that the catalogue entry is wired
to the outside record, not just a name you typed.

## The thing that surprises everyone

Look in the root folder now, and (as installed) there is
**no series folder yet**. This is not a failure. Sonarr's
`createEmptySeriesFolders` setting defaults to off: the
entry reserves its path — `…/media/tv/Dragnet (1951)` — and
the folder itself is created when the first file is
imported into it. Turn the setting on (Settings → Media
Management) if you prefer a folder per entry from day one.
Radarr behaves the same way with its movie folders.

## Read it back

```bash
curl -s -H "X-Api-Key: $SONARR_KEY" http://localhost:8989/api/v3/series
curl -s -H "X-Api-Key: $RADARR_KEY" http://localhost:7878/api/v3/movie
```

Boiled down, the lab's library after chapter 4:

```
Dragnet (1951) | episodes: 276 | on disk: 0
Night of the Living Dead 1968 | monitored: True | hasFile: False
```

A catalogue that knows exactly what it is missing, and a
disk that does not have it yet. Everything after this
chapter is about closing that gap — honestly, and only with
media that is yours to file.
