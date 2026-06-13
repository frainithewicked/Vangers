# Vangers #

![Vangers](http://cdn.akamai.steamstatic.com/steam/apps/264080/header.jpg?t=1447359431)

[![Vangers Linux Build](https://github.com/frainithewicked/Vangers/actions/workflows/vangers_linux_build.yml/badge.svg)](https://github.com/frainithewicked/Vangers/actions/workflows/vangers_linux_build.yml)
[![Vangers Windows 64bit Build](https://github.com/frainithewicked/Vangers/actions/workflows/vangers_windows_64_build.yml/badge.svg)](https://github.com/frainithewicked/Vangers/actions/workflows/vangers_windows_64_build.yml)
[![Vangers Windows 32bit Build](https://github.com/frainithewicked/Vangers/actions/workflows/vangers_windows_32_build.yml/badge.svg)](https://github.com/frainithewicked/Vangers/actions/workflows/vangers_windows_32_build.yml)
[![Vangers MacOS Build](https://github.com/frainithewicked/Vangers/actions/workflows/vangers_macos_build.yml/badge.svg)](https://github.com/frainithewicked/Vangers/actions/workflows/vangers_macos_build.yml)
[![Join the chat at https://t.me/vangers](https://patrolavia.github.io/telegram-badge/chat.svg)](https://t.me/vangers)


Vangers is a video game that combines elements of the racing and role-playing genres.

All source code is published under the GPLv3 license.

While this repository does contain all of the Vangers source code, it does not contain many of the visual assets required to run the game. These assets can be obtained via purchase here:

http://store.steampowered.com/app/264080

http://www.gog.com/game/vangers

## Required libraries ##

* SDL2
* SDL2_net
* libvorbis
* clunk (https://github.com/stalkerg/clunk)
* ffmpeg
* zlib

You can see the [wiki pages](https://github.com/KranX/Vangers/wiki) to learn how to build this project.

## Server

To host a server you can use the Docker image or follow the instructions [here](https://github.com/KranX/Vangers/wiki/Starting-up-server-compatible-with-web-&-native-versions) to do so manually.

To use the docker image you need to pull the `vangers-server` executable and run it like so:

```sh
docker pull caiiiycuk/vangers-server:latest
docker run -v host-dir:container-dir -e SERVER=<server-name> -e CER_FILE=<path-to-cer-file> -e KEY_FILE=<path-to-key-file> caiiiycuk/vangers-server:latest
```

A Vangers server requires cer/key files to host.
For example, if you want to host a server on `vangers.net` and your cer/key files are located in `/root/websockify/`, then your run command will be:

```
docker run -d -v /root/websockify:/root/websockify -e SERVER=vangers.net -e CER_FILE=/root/websockify/vangers.net.cer -e KEY_FILE=/root/websockify/vangers.net.key --network host caiiiycuk/vangers-server
```

Breakdown:
* **-d**: Start in detached mode
* **-v /root/websockify:/root/websockify**: Map the host directory `/root/websockify` to the container directory `/root/websockify`
* **-e SERVER=vangers.net**: Name of the domain you are hosting on
* **-e CERT_FILE=/root/websockify/vangers.net.cer**: Full path to cer file
* **-e KEY_FILE=/root/websockify/vangers.net.key**: Full path to key file
* **--network host**: Specify host networking (required to bind on domain)
