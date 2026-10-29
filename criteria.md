# Writing criteria for this guide

Every "for Mere Mortals" guide is written to the same nine-point
standard, so a reader who trusts one can trust the rest. Here it
is, with the verification notes for this particular guide below.

1. **Fix it first.** Reader outcomes lead, not action items: each
   chapter opens by naming the outcome it delivers, shows a check
   the reader can run to confirm they got it, and a reasonable
   reader finishes able to state what was done, what it means,
   and what to try next.
2. **Plain language.** Short sentences, everyday vocabulary,
   technical terms defined on first use. No slang, and no
   idioms that only make sense in one country — the reader may
   be translating as they go.
3. **No dead ends.** A guide never tells the reader to do
   something it cannot show them how to verify. Every claim a
   reader relies on — an install, a command, an output — is
   something this guide demonstrates or clearly labels
   documented-only below.
4. **Live-verified where it matters.** Procedures are run for
   real in the guide's lab wherever the build machine allows it,
   and the transcripts kept in the repository are the evidence.
   What could not be run is listed honestly below, never
   presented as if it had been.
5. **General audiences.** Nothing in this guide — examples,
   fixtures, names, addresses — is modelled on any particular
   reader or author's real life, network, or organisations.
   The lab's fixtures are a public-domain series and film and
   test videos the lab generated itself.
6. **Standalone.** A reader needs this guide, its lab, and
   nothing else. Where another guide would genuinely help, it
   is pointed to once, by name, and the chapter still completes
   without it.
7. **Honest about limits.** Chapter 12 names what the tools
   cannot do: they hold no content of their own, the catalogue
   is borrowed from outside metadata services, quality is
   graded from the file's numbers and never from viewing it,
   the sample check refuses genuinely short items too, and the
   web interfaces start without a login and are not built for
   the open internet.
8. **The ethics rule is in the text, early.** Chapter 1 and the
   README draw the line plainly, before any procedure depends
   on it — the stack catalogues and organises media the reader
   already owns and supplies nothing itself, and this guide's
   lab used public-domain material and self-made test files
   only, with the download client registered but never sent a
   real job.
9. **Builds clean.** The site builds with MkDocs in strict mode
   with no warnings, and a fresh reader following the chapters
   in order reaches the stated outcome of each.

## Verification notes for this guide

The build machine is a small Ubuntu 24.04 sandbox, shared
with other work while the lab ran. Sonarr **4.0.20.3014**
(branch `main`) and Radarr **6.4.4.10685** (branch `master`)
were installed from the official release archives and run
unmodified, side by side, each with its data folder, media
root folders and a downloads folder inside the lab's own
workspace. Everything was driven through the programs' APIs
with `curl`; the API keys used were the throwaway keys the
lab installs generated, and no transcript in
`arr-stack-lab/transcripts/` contains a real key (the calls
are shown with the key redacted to the word KEY). The
SABnzbd API key used in chapter 8's registration was a
deliberate throwaway, stated as such in the text.

The lab's catalogue fixtures are *Dragnet (1951)* — TVDB id
72763, 9 seasons, 276 episodes — and *Night of the Living
Dead* (1968) — TMDB id 10331, IMDb tt0063350 — both
public-domain works. The "video" imported in chapter 10 is
test material the lab generated with ffmpeg (a test pattern
and a sine tone): real, measurable video files of no
content, at lengths chosen to satisfy the sample check.

Run for real, with transcripts as evidence:

- Downloads of both official archives and the unpacked
  layout (t00); first start of both programs, default
  quality profiles created, listeners on 8989 and 7878.
- Web interfaces: HTTP 200 and `<title>Sonarr</title>` /
  `<title>Radarr</title>`; `/api/v3/system/status` for both
  (versions, branches, OS, SQLite databases); the same call
  without a key refused with 401 (t01).
- Root folders added in both programs and read back, with
  accessible flag and free space (t02).
- Metadata lookups against the live services: four Dragnet
  candidates from Sonarr's SkyHook; the 1968 and 1990 films
  distinguished by TMDB id in Radarr (t03). Posters and
  fanart were then fetched by the programs from the
  services' image servers (session logs).
- Series added with searching off — 9 seasons, 276 episodes
  catalogued, 0 on disk (t04); film added the same way,
  `hasFile: False` (t05); Sonarr's
  `createEmptySeriesFolders: False` default read from its
  media-management config, explaining the absent folder.
- Quality profile edit in Sonarr: HD-1080p cutoff changed
  from 9 (HDTV-1080p) to 7 (Bluray-1080p), upgrades switched
  on, and both read back (t06). Full quality tables for the
  HD-1080p profile printed from both programs, including
  Radarr's film-only qualities (t18).
- Naming configuration read in both programs (formats,
  season and movie folder patterns, renaming off as
  installed), then switched on in both and read back (t07,
  t09).
- Indexers: empty list on a fresh install in both programs;
  the indexer schema (Newznab, Torznab, Torrent RSS and the
  built-in site types) read from Sonarr (t08).
- The import pipeline, three times over: 41-byte stub files
  matched correctly by name and then refused —
  "Unable to determine if file is a sample" (t10);
  real 150-second video refused as "Sample" in both
  programs; full-length stand-ins (25-minute episode,
  40-minute film) accepted with no rejections (t11);
  Sonarr's own debug log quoting the 300-second sample
  minimum (t12).
- Manual import executed through the `ManualImport`
  command: the episode and the film moved into the library
  and renamed by the chapter 9 formats, quality graded from
  the files themselves (the "720p" file filed as SDTV, the
  film as WEBDL-480p), history recording
  `downloadFolderImported` (t13).
- The folder scan mapped: `DownloadedEpisodesScan` pointed
  at a parent downloads folder fails and imports nothing,
  with loose files and with a proper release folder inside
  it (t11, t14); pointed at the single release folder it
  succeeds and imports, renamed, removing the emptied
  folder (t15).
- SABnzbd download client registered in both programs
  (saved disabled, throwaway key, nothing on the port),
  read back, and its connection test run to the genuine
  error — "Unable to connect to SABnzbd, Connection refused
  (127.0.0.1:8080)" — including the two validation
  behaviours on the way: the test route answering 405 for a
  saved-row test, and "Name -> Should be unique" when
  testing a duplicate definition (t16).
- Calendars and scorecards: Sonarr's calendar for
  1951-12-15→18 returning S01E01 with `hasFile: True`;
  Radarr's calendar for the film's 1968 release week with
  its cinema, physical (1978) and digital (2008) dates;
  Wanted/Missing totalling 274 after two of 276 episodes
  were imported; the queue empty (t17).

Documented only — described from the projects' documentation,
not run, and the text does not claim otherwise:

- Registering a real indexer and everything downstream of
  one: RSS sync, interactive and automatic searches that end
  in a real download. The lab holds no indexer account; the
  search *judgement* machinery is the same parsing and
  profiling the import chapters exercised, but no live
  search was performed.
- SABnzbd actually running: a passing connection test, a
  real download, and Completed Download Handling triggered
  by a real client job. The scan the handler calls was
  verified directly (t15) with a locally placed release
  folder.
- Running either program as a system service (systemd
  units, packaged or container installs); the lab ran the
  official binaries in a terminal. Windows and macOS
  installs likewise.
- Custom formats inside quality profiles; hardlink import
  mode (the lab's imports used move); bulk rename/organize
  of an existing library (the preview behaviour is
  described, not executed).
- The neighbours of chapter 11 — Prowlarr, Lidarr, Readarr,
  Bazarr, torrent clients, and media servers such as
  Jellyfin — characterised, not run.

Fixtures are this guide's own and deliberately generic in
kind: two public-domain catalogue entries any reader can
add, and test-pattern video standing in for files the
reader already owns. Nothing in the lab was downloaded from
an indexer or a client, and no real person's media,
accounts or network appear anywhere in it.
