# Importing Files You Already Have

**Outcome:** files sitting in a downloads folder are matched
to the catalogue, judged, moved into the library and renamed
— and you understand the three refusals the lab met on the
way, because each one teaches how the pipeline thinks.

**Check:** the series read-back counts the imported episodes
(`episodes on disk: 2 / 276` in the lab) and the film reports
`hasFile: True` with its new library path.

## The shape of the job

Importing is for media you already hold: recordings you
made, discs you ripped, public-domain files you downloaded
yourself. The programs do not care how the files got there.
They care about three questions, in order:

1. **What is this?** — parse the name for series, season,
   episode (or film and year).
2. **Is it any good?** — open the file, measure it, and check
   it against the quality profile.
3. **Where does it go?** — file it under the root folder,
   renamed (chapter 9), and update the scorecard.

The lab ran this end to end with files it made itself:
ffmpeg-generated video of a test pattern and a tone, named
as releases of the lab's two catalogue entries. The files
are honest stand-ins — real video, of nothing — and the
pipeline treated them exactly as it treats any file, which
is what makes the exercise worth doing.

## Refusal one: "Unable to determine if file is a sample"

The lab's first attempt used 41-byte text files with video
names. The matcher had no trouble at all — right series,
right episode, right film (transcript t10). The refusal
came from the file check:

```
REJECTED: Unable to determine if file is a sample
```

Both programs refuse files they cannot measure. A stub, a
part-download, a renamed text file — anything whose runtime
cannot be read is turned away with this reason, and rightly:
the alternative is a library full of confident pointers to
nothing.

## Refusal two: "Sample"

Real video, then — but only 150 seconds of it. New refusal:

```
REJECTED: Sample
```

The pipeline's **sample check**: a file far shorter than
the thing it claims to be is presumed to be a preview clip.
Sonarr's debug log states its bar plainly — a runtime of
25 minutes "is more than minimum of 300 seconds" and passes
(transcript t12's session log). The lab's fix was to
generate full-length stand-ins: a 25-minute episode file and
a 40-minute film file. Wasteful of nothing but a few
megabytes of test pattern, and the matching call then
reported, for both files:

```
rejections: []
```

The lesson generalises: when an import is refused, the
reason is printed in the manual import screen — read it
before changing anything. The pipeline is picky on purpose,
and it always says why.

## The two ways in

**Manual import** is the front door for loose files. In
Sonarr: **Wanted → Manual Import**; in Radarr: **Movies →
Manual Import** (the same screen also answers to "Library
Import"). Point it at a folder and it lists every video file
with its match and any rejection, as the lab's transcripts
show. Confirm the match — you can correct series, episode or
film per file — choose move or copy, and import. Behind the
screen, the confirmation is a `ManualImport` command; the
lab drove it directly (transcript t13) and the result is
chapter 9's pair of renamed files, plus a history entry:

```
history: downloadFolderImported | dragnet.1951.s01e01.the.human.bomb.720p -> …/media/tv/Dragnet (1951)/Season 1/Dragnet (1951) - S01E01 - The Human Bomb SDTV.mkv
```

**The folder scan** is the automatic door, and it has a
quirk the lab mapped carefully. `DownloadedEpisodesScan`
(and Radarr's `DownloadedMoviesScan`) is the command
Completed Download Handling runs when a client finishes a
job — and the path it wants is **that one download's
folder**, the release folder itself. Pointed at a parent
folder full of downloads, the lab's scans reported
`Failed to import` and imported nothing, twice (transcripts
t11, t14). Pointed at the single release folder, the same
command succeeded at once (transcript t15):

```
status: completed | result: successful
media/tv/Dragnet (1951)/Season 1/Dragnet (1951) - S01E02 - The Big Actor WEBDL-480p.mkv
```

So: a pile of loose files → manual import. One finished
download folder → that is the scan's job, and in daily use
you will never call it by hand, because the download client
integration calls it for you.

## After the import

Read the scorecard back — always. The lab's, after three
imports (transcript t15):

```
Dragnet (1951) | episodes on disk: 2 / 276
Night of the Living Dead | hasFile: True | file: Night of the Living Dead (1968) WEBDL-480p.mkv
```

The downloads folder was empty — move mode had done what it
says. What remains missing is chapter 11's subject: 274
episodes, honestly counted.
