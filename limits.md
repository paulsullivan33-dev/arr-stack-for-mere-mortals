# Limits

**Outcome:** you can state what the stack cannot do, what it
depends on others for, and where its judgement stops —
before any of those surprises you.

**Check:** each limit below names the part of the system it
belongs to. If you can assign them all, you have the map.

## They hold no content

Sonarr and Radarr contain no programmes and no films, and
provide no route to any. They are bookkeeping over a
collection you supply. Any description of them as a way to
"get" television or film is a description of other people's
setups, not of these programs — and this guide's line,
drawn in chapter 1, is a property of the tools themselves.

## The catalogue is borrowed

Everything the programs know about the world comes from
outside metadata services — TheTVDB's data via SkyHook for
Sonarr, TMDB's via Radarr's proxy. Consequences:

- An entry missing or wrong in the source is missing or
  wrong in your catalogue, and the fix belongs upstream.
- Episode numbering follows the source's order. Where a
  series aired in a different order than the catalogue
  lists — a famous nuisance with some shows — the stack
  files by the catalogue, and your player may disagree.
- With no network, existing entries keep working but
  nothing new can be added and nothing refreshes.

## Judgement is name-deep, then file-deep

The pipeline parses names and measures files; it does not
watch anything. A mislabelled file that measures well will
be filed confidently under the wrong episode until a human
notices. Quality is resolution, source and bitrate
arithmetic — a poor transfer at 1080p outranks a fine one
at 720p, because the programs grade the container's numbers,
not the picture. The lab's own imports make the honest
version of this point: test patterns were graded, renamed
and filed flawlessly, because grading was all that was ever
claimed.

## The sample check cuts both ways

Short files are refused as samples (chapter 10). That also
refuses legitimate short things: a two-minute special, a
brief extra, a genuinely short short film can need a manual
push, and a file whose runtime cannot be read at all is
refused whatever it is. The refusal always prints its
reason; overriding it is a manual-import decision, made by
you, per file.

## One machine, one user, home-sized

These are single-household tools. There are no per-user
libraries, no lending, no public catalogue page to share.
The web interfaces start with **no login at all** — right
for a trusted home network, wrong for the open internet.
Do not port-forward them as they are; if you need them away
from home, reach them through your own private network
tooling, and set the authentication options in Settings →
General first.

## The automation stops where you stop it

Monitoring plus an indexer plus a client will, left alone,
act on everything monitored that matches your profiles —
that is the point, and also the limit of the design's
wisdom. The programs do not know your disk is nearly full
until free-space checks trip, do not know a series is one
you meant to drop, and do not ask. Profiles, monitoring
scope and the cutoff are the steering wheel; chapter 12's
weekly check is the glance in the mirror. A stack nobody
steers fills disks with great confidence.

## What this guide could not test

As a limit of the guide rather than the tools: no live
indexer, no real download, and no media server integration
was run in the lab (criteria.md keeps the ledger). The
chapters teach those flows from the projects' documentation
and label them; the verified core — catalogue, profiles,
clients' handshake, import, rename, calendar — is the part
everything else hangs from.
