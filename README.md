# Transmission via Docker container

## Componenets
* Alpine 3.5
* Transmission Daemon 2.92

## Setup

```
$ docker run -d \
    --name=transmission \
    --restart=unless-stopped \
    -e USERNAME=${USERNAME} \
    -e PASSWORD=${PASSWORD} \
    -u <uid>:<gid> \
    -p 9091:9091 \
    -p 54321:54321 \
    -v /media/torrents:/torrents \
    trapexit/transmission
```

By default Transmission setup includes:
* RPC port: 9091
* peer port: 54321
* config-dir: /torrents/.config
* download-dir: /torrents/completed
* incomplete-dir: /torrents/incomplete
* watch-dir: /torrents/.watch
* blocklist-url: http://list.iblocklist.com/?list=bt_level1


When the container is started it will check if `/torrents/.config/settings.json` exists. If it does not it will copy the default there. If you wish to change the settings just stop the container, modify the file, and restart.

`/torrents' should be read, write, & executable by the uid:gid you've set. A mode of 1777 is probably good.

