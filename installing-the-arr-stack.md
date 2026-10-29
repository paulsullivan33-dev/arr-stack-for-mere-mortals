# Installing Sonarr and Radarr

**Outcome:** both programs are running on one machine, each
on its own port, each with its own data folder, and you have
proved both are alive from the command line.

**Check:** the two version calls at the end print Sonarr
4.x and Radarr 6.x, and both web addresses answer 200.

## What you are installing

Both programs ship as self-contained archives for Linux:
everything they need, including their runtime, is inside.
There is nothing to compile and no system package to hunt
down. The lab downloaded the official builds — about
100 MB each:

```bash
curl -sL -o sonarr.tar.gz "https://services.sonarr.tv/v1/download/main/latest?version=4&os=linux&arch=x64"
curl -sL -o radarr.tar.gz "https://radarr.servarr.com/v1/update/master/updatefile?os=linux&runtime=netcore&arch=x64"
mkdir -p sonarr radarr
tar -xzf sonarr.tar.gz -C sonarr --strip-components=1
tar -xzf radarr.tar.gz -C radarr --strip-components=1
```

Unpacked, each takes a little over 230 MB of disk. Keep the
two in separate folders: they are different programs that
happen to share many file names.

## The data folder is the program's memory

Each program keeps everything it knows — its database, its
configuration, its logs, its API key — in a **data folder**
you choose with the `-data` switch. Keep data out of the
program folder: when you later unpack a newer release over
the program folder, your library's memory survives.

The lab ran both in the foreground of a terminal, like this:

```bash
./sonarr/Sonarr -data=/home/user/arr-data/sonarr -nobrowser
./radarr/Radarr  -data=/home/user/arr-data/radarr -nobrowser
```

`-nobrowser` stops the program trying to open a browser on
a machine that may not have one. In daily use you would run
them as services instead — both projects document systemd
units, and on many systems a package or a container does
this for you; the shape is the same either way: program
folder, data folder, port. Those service setups are
documented-only in this guide; everything after this chapter
was run against the plain binaries above.

A healthy start ends with lines like these (transcript t01's
session log):

```
[Info] Microsoft.Hosting.Lifetime: Now listening on: http://[::]:8989
[Info] QualityProfileService: Setting up default quality profiles
```

Radarr listens on 7878 in the same way.

## First contact: the two ports

Sonarr's web interface is at `http://localhost:8989` and
Radarr's at `http://localhost:7878`. A fresh install asks
for no password — that is normal on a home network and a
reason, covered in chapter 12, not to expose these ports to
the internet as they are.

The lab's first checks, and yours:

```bash
curl -s -o /dev/null -w "%{http_code}\n" http://localhost:8989/
curl -s http://localhost:8989/ | grep -o "<title>[^<]*</title>"
curl -s -o /dev/null -w "%{http_code}\n" http://localhost:7878/
curl -s http://localhost:7878/ | grep -o "<title>[^<]*</title>"
```

```
200
<title>Sonarr</title>
200
<title>Radarr</title>
```

## The API key

On first run each program generates an **API key** and
writes it into `config.xml` inside its data folder. It is
the password for the program's API — treat it like one, and
do not paste it into shared notes. Load yours into shell
variables once, the way this guide's lab did, and the rest
of the guide's commands can use them:

```bash
SONARR_KEY=$(grep -o '<ApiKey>[^<]*' /home/user/arr-data/sonarr/config.xml | sed 's/<ApiKey>//')
RADARR_KEY=$(grep -o '<ApiKey>[^<]*' /home/user/arr-data/radarr/config.xml | sed 's/<ApiKey>//')
```

With the key, the version check that proves the whole
installation:

```bash
curl -s -H "X-Api-Key: $SONARR_KEY" http://localhost:8989/api/v3/system/status
curl -s -H "X-Api-Key: $RADARR_KEY" http://localhost:7878/api/v3/system/status
```

The lab's answers (transcript t01) named Sonarr
**4.0.20.3014** on branch `main` and Radarr **6.4.4.10685**
on branch `master`, both on Ubuntu 24.04, each with its
database type reported as SQLite. Without the key, the same
call is refused:

```bash
curl -s -o /dev/null -w "%{http_code}\n" http://localhost:8989/api/v3/system/status
```

```
401
```

That 401 is a feature to verify, not a problem to fix: it
proves the key is doing its job.
