# Renaming and Organising the Library

**Outcome:** renaming is switched on in both programs, you
can read the naming formats they will use, and you know
exactly what name an imported file ends up with.

**Check:** the naming read-back shows `renameEpisodes:
True` and `renameMovies: True`, and chapter 10's imported
files carry the formats shown here.

## Why the library end needs manners

Downloads arrive named for the release, not for you:
`dragnet.1951.s01e01.the.human.bomb.720p.mkv`. A media
server, a human, and the *arr programs themselves all do
better with a name that states the series, the episode and
the quality in a fixed shape. Renaming is the import
pipeline's last act: as a file is filed, it is renamed to
the pattern.

## The formats, as installed

Settings → Media Management holds them. The lab read both
programs' defaults (transcript t07):

Sonarr:

```
standardEpisodeFormat: {Series Title} - S{season:00}E{episode:00} - {Episode Title} {Quality Full}
seriesFolderFormat:    {Series Title}
seasonFolderFormat:    Season {season}
```

Radarr:

```
standardMovieFormat: {Movie Title} ({Release Year}) {Quality Full}
movieFolderFormat:   {Movie Title} ({Release Year})
```

The tokens in braces are filled from the catalogue entry —
which is why a file renamed by the program can be trusted
in a way the release name cannot: the title, year and
episode name come from the metadata record, and the quality
comes from measuring the file (chapter 5's caution). You
can edit the patterns — add the year to a series folder,
drop the quality, and so on — and both programs show a live
example as you type. Keep `{Quality Full}` somewhere in the
pattern: it is the one part of the name that records what
the program measured, and future-you will want it.

## It starts switched off

As installed, both programs have renaming **off**
(`renameEpisodes: False`, `renameMovies: False` in the same
transcript). Files are imported under their release names
until you say otherwise. The lab switched both on through
the API and read the change back (transcript t09):

```
renameEpisodes now: True
renameMovies now: True
```

Switching renaming on changes nothing already in the
library. It applies at import time — and to anything you
later ask the program to rename in bulk (Series → select →
Rename, and Radarr's Organize), which previews every change
before applying it. Use the preview; it is the check this
chapter offers for library-wide operations.

## What an imported file is called

With renaming on, the lab's two imports landed as
(transcript t13):

```
media/tv/Dragnet (1951)/Season 1/Dragnet (1951) - S01E01 - The Human Bomb SDTV.mkv
media/movies/Night of the Living Dead (1968)/Night of the Living Dead (1968) WEBDL-480p.mkv
```

Every promise of the formats is visible in those two lines:
series folder from the catalogue title, a `Season 1`
folder, episode title spelled as the metadata spells it —
and the quality the *file* earned (SDTV, WEBDL-480p), not
the one its release name advertised. If you take one idea
from this guide, take that pairing: **the catalogue names
it, the file grades it.**

## House rules worth adopting

- **One root folder per kind of media**, on the disk you
  actually back up. The library the programs organise is
  only as safe as the folder it lives in.
- **Let the program move files; do not move them yourself.**
  A file moved by hand is a file the catalogue now believes
  is missing. If you must rearrange disks, change the root
  folder in the program and let it re-file.
- **Hardlinks**, offered in the same settings screen, let a
  finished download and the library copy be one file on disk
  with two names — worth it on large libraries, and only
  possible when downloads and library share a filesystem.
  The lab imported with plain moves and did not test
  hardlink mode; it is documented-only here.
