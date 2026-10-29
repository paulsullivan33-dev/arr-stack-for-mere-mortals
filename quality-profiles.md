# Quality Profiles and Cutoffs

**Outcome:** you can read a quality profile the way the
program does — a ranked list with a stopping point — and
change one, then read the change back.

**Check:** after the lab's edit below, the read-back shows
the new cutoff and upgrades switched on. If yours still
shows the old values, the edit never landed.

## What a quality is

A **quality** is the program's name for how good a file is:
where it came from and at what resolution. SDTV and DVD at
the bottom; HDTV-720p, WEBDL-720p and Bluray-720p in the
middle; the 1080p set above them; the 2160p (4K) set and
remuxes — bit-for-bit copies of a disc — at the top. Radarr
adds rows Sonarr has no use for: CAM, TELESYNC and WORKPRINT,
the film world's rough in-cinema and pre-release sources.

Two cautions the lab demonstrated rather than assumed:

- Quality is judged from the **file**, not its name. The
  lab imported a file whose name claimed 720p; its picture
  was really 320×180, and the library recorded it as SDTV
  (transcript t13). Names are advertising; the program
  measures.
- The two programs share quality *names*, but each keeps its
  own list and numbering. Never copy an id from one program
  into the other and expect it to mean the same row — check
  the table (transcript t18 prints both).

## The shape of a profile

A **quality profile** is one ranked list plus three
decisions (Settings → Profiles in either program):

1. **Allowed** — the qualities the program will accept at
   all. A release in a disallowed quality might as well not
   exist.
2. **Cutoff** — the quality that counts as *good enough*.
   Once a file at the cutoff (or better) is on disk, the
   program stops wanting more for that episode or film.
3. **Upgrades allowed** — whether a better file below the
   cutoff should replace the one on disk when it appears.

The six starter profiles are the same in both programs:
**Any**, **SD**, **HD-720p**, **HD-1080p**, **Ultra-HD** and
**HD - 720p/1080p**. As installed, the lab found them all
with upgrades *off* — a first file is kept as it lands
(transcript t02). That is a defensible default: predictable
disk use, no churn. Turn upgrades on when you would rather
the library quietly improve itself toward the cutoff.

## The lab's edit, and its read-back

The lab took Sonarr's HD-1080p profile — installed with
cutoff **9 (HDTV-1080p)** — and changed it to cutoff **7
(Bluray-1080p)** with upgrades allowed, the "keep improving
until it is genuinely good" setting (transcript t06):

```bash
curl -s -H "X-Api-Key: $SONARR_KEY" http://localhost:8989/api/v3/qualityprofile/4
```

```
cutoff: 9 | upgradeAllowed: False
```

…the edit sent back with those two fields changed, and the
same call again afterwards:

```
cutoff: 7 | upgradeAllowed: True
```

The read-back is the check: a profile edit you cannot read
back is an edit you only hope happened.

## Choosing a profile with your eyes open

- **Match the display, not the dream.** A 720p profile on a
  small screen costs a third of the disk of 1080p and looks
  the same from the sofa.
- **Cutoff is a disk decision.** Every step up the list is
  paid for in gigabytes, per episode, per season. Ultra-HD
  for a 276-episode series is a purchase, not a preference.
- **One profile per entry, changeable any time.** Changing
  a profile does not touch files on disk; it changes what
  the program will look for and accept from now on. Nothing
  is re-filed, nothing is deleted.
- **Custom formats** — a finer scoring layer inside profiles,
  for preferences like particular release groups or audio
  setups — are a real feature of both programs and are
  documented-only in this guide: the lab did not build any,
  and the chapters do not pretend otherwise.
