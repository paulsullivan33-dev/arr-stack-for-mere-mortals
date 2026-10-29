# Connecting a Download Client

**Outcome:** a SABnzbd client is registered in both Sonarr
and Radarr, with a category in each, and you have seen
exactly what a failed connection test says — so a real one
will never puzzle you.

**Check:** the client list read-back shows the client saved
in each program, and the test at the end produces the
connection error quoted below when nothing is listening.

## Why a client at all

Chapter 2's shape: the *arr programs decide; the **download
client** fetches. Registering a client is telling Sonarr
and Radarr where to send work and how to label it. For
Usenet that client is SABnzbd, whose own guide in this
series covers running it; this chapter is the handshake
between the two.

In either program: **Settings → Download Clients → + →
SABnzbd**. The fields that matter:

- **Host and port** — where SABnzbd listens; `127.0.0.1`
  and `8080` when they share a machine.
- **API key** — SABnzbd's own key, from its Config →
  General page. Each program holds the other's key: that
  is the whole trust arrangement.
- **Category** — the label attached to jobs this program
  sends. Sonarr's form calls it the TV category (`tv`);
  Radarr's, the movie category (`movies`). SABnzbd files
  finished jobs by category, and chapter 10's import
  pipeline keys off the result.
- **Priorities** — separate knobs for recent and older
  material, so a current episode can jump SABnzbd's queue
  ahead of a back-catalogue season.

## The lab's registration

The lab registered SABnzbd in both programs through the API
(transcript t16) with a throwaway key, deliberately with
**nothing listening on port 8080**, and with the client
saved *disabled*. Both programs accepted and stored the
definition:

```
saved: id 1 | name: SABnzbd (lab) | implementation: Sabnzbd | enable: False | protocol: usenet
```

Saving a disabled client is a useful pattern in itself:
the definition is in place, the read-back proves it, and
nothing will try to use it until you enable it.

## The test button tells the truth

Every client form has a **Test** button, and it is the most
honest button in either program: it makes a real connection
attempt and reports what happened. Against the lab's
empty port, Sonarr's answer (transcript t16) was:

```
Host -> Unable to connect to SABnzbd
Test was aborted due to an error: Unable to connect to SABnzbd, Connection refused (127.0.0.1:8080)
```

Read a failure like that literally. *Connection refused*
means the address answered but no program was listening —
SABnzbd is not running, or is on a different port. It does
**not** mean the API key is wrong; a wrong key gets further
and fails differently, with an authentication complaint from
SABnzbd itself. Two different failures, two different
fixes, and the message tells you which one you have.

Two more behaviours the lab met on the way, worth knowing
before they surprise you:

- Testing a definition whose **name is already saved**
  fails validation with `Name -> Should be unique` before
  any connection is attempted. Rename the copy, or test
  from the saved client's own edit screen.
- The test route expects the **whole definition** posted to
  it — which is what the settings screen does. It is a
  check of a form, not of a saved row.

## Once it connects

With SABnzbd actually running and the test passing, enable
the client. From then on the flow this guide has been
building toward is automatic: a search (chapter 7) picks a
release, the release is sent to SABnzbd under the category,
SABnzbd downloads and unpacks it, and the import pipeline
(chapter 10) files it into the library. The **Queue** page
in Sonarr or Radarr shows jobs in flight — the lab's queue,
with no client enabled and nothing sent, read back as the
honest figure in transcript t17:

```
queue records: 0
```

This guide's lab stopped at the handshake: no real download
was sent, by design (chapter 1's line). The connection test
against a *running* SABnzbd, and everything downstream of a
passing one, is documented-only here — follow SABnzbd's own
guide to bring the client up, then use the test button as
your check.
