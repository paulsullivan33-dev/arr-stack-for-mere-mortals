# Glossary

**API key** — The password a program generates for its own
API. Sonarr's and Radarr's live in `config.xml` in each data
folder; SABnzbd has one of its own. Each program holds the
others' keys where they need to talk.

**Calendar** — The catalogue viewed by date: air dates in
Sonarr, cinema/physical/digital release dates in Radarr.

**Catalogue** — In this guide, the program's record of what
exists in the world: every season and episode of a series,
every release date of a film. Kept from metadata services,
not from your disk.

**Category** — The label attached to jobs sent to a download
client (`tv`, `movies`), used by the client to file finished
work and by the stack to recognise it.

**Completed Download Handling** — The machinery that watches
a download client, notices a finished job, and hands its
folder to the import pipeline.

**Cutoff** — The quality at which a profile is satisfied.
Below it, upgrades are wanted; at it, the wanting stops.

**Data folder** — Where a program keeps its database,
config and logs, set with `-data` at launch. Separate from
the program folder so upgrades do not touch memory.

**Download client** — The program that fetches: SABnzbd for
Usenet, or a torrent client. The stack decides; the client
fetches.

**Has file** — The scorecard's word for an entry satisfied
by a file on disk (`hasFile: True`).

**Import pipeline** — The parse → measure → decide → file →
record path a finished or existing file travels into the
library.

**Indexer** — A searchable catalogue of releases that exist
in the world. Sonarr and Radarr query indexers; they are not
indexers themselves.

**Library** — The files you actually have, organised under
the root folders.

**Manual import** — The screen (and command) for matching
files you already have to catalogue entries by hand, with
rejections and reasons shown.

**Metadata service** — The outside source of catalogue data:
TheTVDB's data via Sonarr's SkyHook proxy; TMDB's via
Radarr's proxy.

**Minimum availability** — Radarr's setting for which of a
film's release dates counts as "out": announced, in cinemas,
physical/digital release.

**Monitored** — Marked as *care about the gap*: a monitored,
aired, fileless entry counts as missing and is searched for.

**Newznab / Torznab** — The standard dialects the stack uses
to question Usenet indexers and torrent sites respectively.

**Quality** — The program's grade for a file — SDTV, HDTV-720p,
WEBDL-1080p, Bluray-1080p, remux — measured from the file,
not believed from its name.

**Quality profile** — A ranked list of qualities with an
allowed set, a cutoff, and an upgrades decision, assigned
per series or film.

**Release** — One named, sized, quality-claiming copy of an
episode or film out in the world — the unit indexers list
and clients fetch.

**Remux** — A file whose audio and video are copied
bit-for-bit from a disc into a new container. Top of the
quality list, and priced in disk accordingly.

**Root folder** — A directory a program may file media into:
one for series, one for films, at minimum.

**RSS search** — The background habit of reading indexers'
recent-release feeds and matching them against the monitored
missing list.

**Sample** — A too-short preview file, and the pipeline's
refusal of one. An episode under 300 seconds of runtime is
presumed to be one.

**Season 0** — Where specials live in a series' catalogue.

**SkyHook** — Sonarr's metadata proxy, serving TheTVDB data
in the shape Sonarr consumes.

**TMDB / TVDB id** — The stable numbers identifying a film
or series in the metadata services. Titles repeat; ids do
not.
