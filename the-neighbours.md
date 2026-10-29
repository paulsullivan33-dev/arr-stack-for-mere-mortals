# The Neighbours

**Outcome:** you can place the stack among the tools around
it — what each neighbour does that Sonarr and Radarr don't,
and the one cousin worth knowing about.

**Check:** for each neighbour, name the hand-off point: what
crosses the boundary between it and the stack.

## SABnzbd — the hands

SABnzbd downloads from Usenet: it takes an NZB file, fetches
the articles, repairs, unpacks, and leaves a finished folder.
Sonarr and Radarr never touch that machinery. The hand-off
is chapter 8's registration — the stack sends a release to
SABnzbd under a category, SABnzbd does the fetching, and
Completed Download Handling hands the finished folder to the
import pipeline. SABnzbd has its own guide in this series;
the two together are the complete Usenet shape: SABnzbd is
the hands, the stack is the memory.

Neither replaces the other. SABnzbd alone leaves you a
downloads folder and your own filing. The stack alone is a
catalogue of good intentions. The pair is the tool.

## Torrent clients — the other hands

Everything chapter 8 says about SABnzbd has a mirror for
torrent clients (qBittorrent, Deluge, Transmission and
others appear in the same Download Clients list). The stack
is even-handed: it sends work to whichever client you
register, seeds and all, and imports the result the same
way. This guide registered the Usenet client because the
series' Usenet guide gives it context; the mechanics on the
stack's side are identical.

## Prowlarr — the switchboard cousin

Register five indexers in Sonarr and the same five in
Radarr and you will maintain ten definitions. **Prowlarr**
exists to make that one: it is the family's indexer manager,
holding every indexer definition once and syncing them into
each *arr program. It also searches all of them from its own
screen. If you run the stack with more than one or two
indexers, Prowlarr is the difference between a hobby and a
chore — and it deserves, and will need, a guide of its own;
this one only points at it.

## A media server — the stage

The library the stack organises is meant to be watched, and
that is a media server's job (Jellyfin, Plex, Emby and their
kin). The hand-off is the folder structure itself: the
stack's root folders are the media server's libraries, and
chapter 9's renaming discipline is precisely what makes the
server's own matching effortless — a server pointed at an
*arr-organised library finds clean titles, years and episode
numbers instead of release names. Keep the two on the same
folders and neither needs to know the other exists.

## Doing it by hand — the baseline

Everything the stack does can be done by a person with a
spreadsheet and patience: track the episode lists, rename
the files, count the gaps. For twelve files, do that — it
is less machinery. The stack earns its place when the
collection outgrows memory: hundreds of episodes, three
release dates per film, quality judgements applied the same
way every time. Automation here is not about speed; it is
about the bookkeeping being *the same* on the thousandth
file as on the first, which no human filing habit honestly
is.

## The wider family

Lidarr (music), Readarr (books) and Bazarr (subtitles, a
close companion rather than a sibling) apply the same shape
to other shelves. This guide does not cover them; if you
have learned Sonarr and Radarr from it, you already know
their grammar — catalogue, profile, indexer, client, import —
and only the vocabulary changes.
