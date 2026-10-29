# Calendars and Monitoring

**Outcome:** you can read each program's calendar, say what
the **monitored** switch really commits the program to, and
use the missing list as the honest centre of the whole
system.

**Check:** the calendar calls below find the lab's episode
on its original 1951 air date — marked as having a file,
because the lab imported it — and the film in its 1968
release week.

## The calendar is the catalogue, dated

Both programs keep a calendar: Sonarr's is episodes by air
date, Radarr's is films by release date. It is not a
separate diary you maintain; it is the catalogue viewed
sideways, which means it is correct for dates you would
never type in yourself. The lab asked Sonarr for the weekend
its episode first aired — seventy-five years before the
lab ran (transcript t17):

```
S01E01 | The Human Bomb | aired: 1951-12-16T05:00:00Z | hasFile: True
```

And Radarr for the film's opening week:

```
entries: 1
Night of the Living Dead | inCinemas: 1968-10-04 | physicalRelease: 1978-10-24 | digitalRelease: 2008-02-19
```

Three dates for one film, each the start of a different
kind of availability — which is why Radarr's **minimum
availability** setting exists (chapter 4): it tells the
program which of those dates makes a film "out" for your
purposes. A film can be in the catalogue for months before
its date arrives; the calendar is where you watch it come.

In daily use the calendar answers the only schedule question
that matters — *what lands this week, and do I have it?* —
for series you follow and films you are waiting on, with
the has-file flag doing the second half of the sentence.

## Monitored means "care about the gap"

**Monitoring** is the switch that connects the catalogue to
the machinery. A monitored episode that has aired and has
no file is a candidate: it appears in searches, it is
matched against indexer RSS (chapter 7), it counts as
missing. An unmonitored one is merely known about.

The controls are finer than one switch:

- per **series** and per **season** in Sonarr — follow a
  show but skip its weak third season entirely;
- per **episode**, for the one you never liked;
- per **film** in Radarr;
- and a series-level choice of *which* episodes get
  monitored when you add it — all, future only, the latest
  season, or none.

The lab monitored everything it added, and Radarr's and
Sonarr's editors both let you change your mind per item
afterwards — monitoring is a stance, not a contract.

## The missing list

**Wanted → Missing** in Sonarr (and Radarr's equivalent
view) is the scorecard made visible: monitored, aired,
fileless. The lab's read-back (transcript t17):

```
total missing (monitored, aired, no file): 274
 e.g. S01E03 The Big Death | monitored: True
 e.g. S01E04 The Big Mother | monitored: True
 e.g. S01E05 The Big Cast | monitored: True
```

276 catalogued, 2 imported, 274 missing — the arithmetic
always balances, and that is the point of the whole stack.
This list is what RSS search works on, what an automatic
search drains, and what your eye should check weekly
(chapter 12's recipe). It is also, note, entirely about
bookkeeping: the list says your library lacks these files.
How any of them would legitimately arrive — your own
recordings, your own discs, public sources for public-domain
material — is your side of the line the guide drew in
chapter 1.

## A quiet word about continuing series

For a series still on air, this chapter is the whole
product: add it monitored with "future episodes" scope, and
the calendar plus the missing list become a reliable
programme guide for your own recording and filing habits.
For an ended series like the lab's, the same machinery is a
checklist. Either way, nothing in this chapter reaches out
and takes anything — it watches, counts, and waits for the
import pipeline to close the gap.
