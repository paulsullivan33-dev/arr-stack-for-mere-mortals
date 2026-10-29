# What the *arr Stack Is

**Outcome:** you can say what Sonarr and Radarr each keep
track of, what they deliberately do not do, and why the pair
is treated as one tool with two heads.

**Check:** at the end, name the three jobs both programs do —
catalogue, compare, organise — and the one job neither does:
supply the media itself.

## Two librarians

Sonarr and Radarr are library managers.

- **Sonarr** manages **television series**. Its world is
  seasons and episodes, air dates, and the slow drip of new
  episodes over years.
- **Radarr** manages **films**. Its world is single works
  with release dates — cinema, then physical, then digital —
  and editions.

Each program keeps three things:

1. **A catalogue** of what exists. Add a series and Sonarr
   fetches its full episode list — the lab added *Dragnet*
   (1951) and was handed 9 seasons and 276 episodes, none of
   them files yet. Add a film and Radarr fetches its release
   dates, its identifiers, and its poster.
2. **A library** of what you have. Point the program at a
   **root folder** — the place your media lives — and it
   tracks which catalogue entries are satisfied by a file on
   disk, and at what quality.
3. **A scorecard** of the gap. What is monitored, aired, and
   still missing is a list the program maintains for you.
   After the lab imported two episodes, Sonarr's missing
   list stood at 274 — the arithmetic is the service.

On top of that bookkeeping sits machinery this guide takes
in order: **quality profiles** decide how good a file must
be before the program is satisfied; **indexers** are
catalogues of releases it can search; **download clients**
(such as SABnzbd) fetch things on its behalf; and the
**import pipeline** moves finished files out of the
downloads folder, renames them, and files them in the
library.

## What they share, and where they part

The two programs are siblings, not twins — they come from
the same codebase family and it shows:

| | Sonarr | Radarr |
|---|---|---|
| Looks after | TV series | Films |
| Unit of work | The episode | The film |
| Default port | 8989 | 7878 |
| Metadata comes from | TheTVDB, via Sonarr's SkyHook proxy | TMDB, via Radarr's proxy |
| Stable identity | TVDB id | TMDB id (and IMDb id) |
| Calendar shows | Air dates | Cinema, physical and digital release dates |
| Quality list extras | Broadcast and web qualities | Film-source qualities too — CAM, TELESYNC, WORKPRINT |

The differences that matter day to day are the ones the
table's middle rows name. A series is never "done" the way a
film is: it has a status (continuing or ended), seasons you
may or may not monitor, and specials that live in "season 0".
A film is one file (plus the question of which edition), but
it has *three* birthdays, and Radarr's **minimum
availability** setting exists to say which birthday counts.

## The line this guide keeps

Neither program contains, hosts, or sells a single episode
or film. They are indexes and filing clerks for a collection
you hold yourself. The lab in this guide therefore worked
with:

- a public-domain series and film whose copyright status is
  not in dispute,
- home-made test videos generated with ffmpeg, and
- a download client registered but never sent a real job.

That is not a limitation of the guide; it is the honest
shape of the tool. Everything the stack does for a
hundred-episode collection it also does for twelve home
videos and a shelf of classics — the bookkeeping is the
product.

## What runs where

Each program is a self-contained application with a web
interface. You run it on one machine — often the machine
that holds the media — and drive it from a browser, on the
same machine or across your home network. There is no
account to create with the projects, no subscription, and
no phone-home in normal use beyond fetching metadata and
checking for its own updates. Underneath the web pages sits
a full **API** (application programming interface): every
click in the interface is an API call, which is why this
guide's lab could drive both programs from the command line
and keep the receipts.
