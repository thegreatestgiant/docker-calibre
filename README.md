# DEPRICATED

Linuxserver has upgraded to using selkies instead of kasmvnc, which introduced breaking changes.
It now requires https which breaks a lot of my config so I'm going to retire the project. The latest working version is 99. Here is the cli code to run it.

```bash
docker run -d \
  --name=calibre \
  --security-opt seccomp=unconfined \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/New_York \
  -p 8080:8080 \
  -p 8081:8081 \
  -v config:/config \
  --restart unless-stopped \
  thegreatestgiant/calibre:99
```

# Docker-Calibre

### docker cli

```bash
docker run -d \
  --name=calibre \
  --security-opt seccomp=unconfined \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=America/New_York \
  -p 8080:8080 \
  -p 8181:8181 \
  -p 8081:8081 \
  -v config:/config \
  --restart unless-stopped \
  thegreatestgiant/calibre
```

## docker-compose

```yaml
---
version: "2.1"
services:
  calibre:
    image: thegreatestgiant/calibre
    container_name: calibre
    security_opt:
      - seccomp:unconfined
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_york
    volumes:
      - ./config:/config
    ports:
      - 8080:8080
      - 8181:8181
      - 8081:8081
    restart: unless-stopped
```

## Links To Heal Epubs

```
https://kindle-epub-fix.netlify.app/
```

_(Not as good)_

```
https://draft2digital.com/book/epubcheck/upload
```

# Updating

```
git clone https://github.com/thegreatestgiant/docker-calibre.git && cd docker-calibre
```

do that into home linux and then upload the files again
also add rsync to dockerfile

OR

```
git config pull.rebase true
git pull https://github.com/linuxserver/docker-calibre.git
git config --local rerere.enabled true
```

For rebasing you have to git add and rm and for things that modify both you can generally do

```
git checkout --ours .
```

and if it doesn't work then do

```
git restore --theirs .
```
