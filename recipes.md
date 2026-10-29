# Recipes

**Outcome:** four small, complete setups that combine the
chapters into working habits.

**Check:** each recipe ends with the read-back or screen
that proves it is in place.

## 1. The tidy starter setup

For a fresh install, in order:

1. Add one root folder per program (chapter 4) — television
   and films on the disk you back up.
2. Leave the six starter profiles alone except one choice:
   in your main profile, decide about **upgrades**
   (chapter 5). Off is predictable; on is self-improving.
3. Switch **renaming on** in both programs (chapter 9)
   before the first import, so no file ever lands under a
   release name.
4. Register the download client **disabled** (chapter 8),
   run its test against the real client when the client is
   up, and only then enable it.

Check: the client list shows your client enabled, the
naming read-back shows renaming true, and the root folder
call reports `accessible: true`.

## 2. Filing recordings you made yourself

The stack's sweet spot for media you produced: broadcasts
you recorded, and discs you ripped, where the result matches
a catalogue entry.

1. Add the series or film by search (chapter 4), monitored,
   with search-on-add off.
2. Put your recording in the downloads folder under its
   plain name — the matcher reads names like
   `Dragnet.1951.S01E03.mkv` without help.
3. Manual import it (chapter 10). If the matcher pairs it
   with the wrong episode, correct the pairing on the
   manual import screen before confirming — that screen
   exists for exactly this.
4. Purely personal footage — family video, your own
   projects — does not belong here: it has no catalogue
   entry, and the catalogue is the product. Keep it in
   plain folders, backed up the ordinary way.

Check: the entry's calendar line flips to `hasFile: True`,
and the missing count drops by exactly the number of files
you imported.

## 3. A public-domain classics shelf

For material whose copyright has lapsed or was never
registered — much early television and a good shelf of
classic film:

1. One root folder pair, classics only.
2. Add by search (chapter 4), choosing by TVDB/TMDB id;
   public-domain staples are all in the catalogues.
3. A dedicated quality profile: duplicate HD-1080p, set its
   cutoff lower (these sources are rarely better than DVD
   quality), and assign it to the classics so the programs
   stop wanting upgrades that do not exist.
4. File the copies you lawfully download yourself through
   manual import (chapter 10).

Check: the missing list counts only what you have not yet
filed, and the profile read-back shows the classics profile
on the classics entries.

## 4. The weekly five-minute check

The stack mostly runs itself; this is the whole maintenance
habit:

1. Open **Wanted → Missing** in Sonarr and the matching view
   in Radarr. Anything unexpected there is either a file you
   moved by hand (chapter 13) or a monitoring choice to
   revisit (chapter 11).
2. Glance at **System → Status** in each: version, and any
   health warnings (a root folder gone missing announces
   itself here first).
3. Glance at the **Queue**: anything stuck has a reason
   printed on it.
4. Confirm the root folders' free space is not trending to
   zero — quality cutoffs are disk decisions (chapter 5),
   and the library grows by your choices, not by accident.

Check: missing counts you can explain, a queue you can
explain, and free space you can explain. Five minutes,
weekly, is genuinely all of it.
