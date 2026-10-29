# Troubleshooting

**Outcome:** the six failures this guide's lab actually met
— plus the two everyone meets — each with its cause and its
check.

**Check:** every entry below ends with the read-back that
proves the fix. If a fix has no check, it is a hope, not a
fix.

## "I added a series and there is no folder for it"

Not a fault. As installed, Sonarr's `createEmptySeriesFolders`
is off (Radarr behaves alike), so the folder is created at
first import, not at add time. Check the entry's reserved
path instead:

```bash
curl -s -H "X-Api-Key: $SONARR_KEY" http://localhost:8989/api/v3/series
```

The `path` field is the promise; the folder follows the
first file. Or turn the setting on under Settings → Media
Management (transcript t05).

## "Manual import says: Unable to determine if file is a sample"

The program could not read a runtime from the file — it is
a stub, a part-download, a subtitle file wearing a video
name, or plain not-video. Check the file yourself:

```bash
ffprobe -v error -show_entries format=duration -of csv=p=0 "the-file.mkv"
```

If ffprobe cannot read it either, the program is right
(transcript t10). Replace the file; there is no setting
that makes an unreadable file importable, and you would not
want one.

## "Manual import says: Sample"

The file is real video but far shorter than the episode or
film it claims to be — Sonarr's bar, from its own log, is a
300-second minimum runtime for an episode (transcript t12).
Shorts and brief extras trip this honestly. If the file is
genuinely the whole item, say so on the manual import screen
and import it as a deliberate act; if it is a preview clip,
the program just saved your library from it.

## "The folder scan completed but imported nothing"

`DownloadedEpisodesScan` / `DownloadedMoviesScan` want the
path of **one finished download — the release folder
itself** — not the folder full of downloads. Pointed at the
parent, the lab's scans reported `Failed to import` and did
nothing, repeatably (transcripts t11, t14). Pointed at the
release folder, the same command succeeded immediately
(transcript t15). For a mixed pile of loose files, use
manual import instead; that is what it is for.

## "The download client test fails"

Read the message literally; it names its own layer
(transcript t16):

- `Connection refused` — nothing is listening at that host
  and port. The client is down, or the port is wrong.
- An authentication complaint — you reached the client; the
  API key is wrong. Keys live in the client's own settings
  (SABnzbd: Config → General).
- `Name -> Should be unique` — you tested a copy of a
  definition whose name is already saved. Test from the
  saved client's edit screen, or rename the copy. This one
  fires before any connection is attempted, and it fooled
  the lab first, too.

## "It imported, but at the wrong quality"

It didn't misjudge; it measured. Quality comes from the
file's real resolution and source, not its name — the lab's
"720p" file was 320×180 and was filed as SDTV (transcript
t13). If the *file* is genuinely better than its grade,
check it with ffprobe; if ffprobe agrees with the program,
the release name was the lie.

## "Episodes are numbered wrong"

The catalogue's order rules (chapter 12): Sonarr files by
TheTVDB's episode list as served by SkyHook, including its
season 0 for specials. A file named for a different order —
DVD order is the classic case — will match the "wrong"
episode with complete confidence. Fix the pairing per file
on the manual import screen, and for a whole series use the
series' numbering options where the program offers them.

## "Everything was fine and now files show as missing"

You moved them, or a disk did not mount, or a root folder
path changed. The catalogue only believes the disk it can
see: check the root folder call for `accessible: true`,
check the disk is mounted at the same path, and let a
rescan (Tasks, or the series' refresh) reconcile before
re-importing anything. Re-importing into a second location
is how libraries fork; reconcile first.
