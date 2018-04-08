# Friendly Audio Streaming Protocol (FASP)

A simple and open **protocol for streaming audio in local networks**.

Sort of like [*AirPlay*](https://nto.github.io/AirPlay.html#introduction) and *DLNA*, but

- code & spec are openly available
- no [DRM](https://en.wikipedia.org/wiki/Digital_rights_management)
- un-overengineered: ~~XML~~ JSON, ~~[reverse HTTP](https://tools.ietf.org/id/draft-lentczner-rhttp-00.txt)~~ [WebSockets](https://en.wikipedia.org/wiki/WebSocket)
- flexible: any client can control playback & play new media

**If you want to try it out, head over to [Getting started](getting-started.md).**

![CC-licensed](https://img.shields.io/github/license/public-transport/friendly-public-transport-format.svg)
[![chat on gitter](https://badges.gitter.im/public-transport/Lobby.svg)](https://gitter.im/public-transport/Lobby)

## How it works

A FASP *receiver* is a WebSocket server. Any number of *clients* can connect to it and send the following commands, encoded as JSON:

- `['play', 'http://example.org/some-url']`
- `['queue', 'http://example.org/some-url']`
- `['next']`
- `['previous']`
- `['play-pause']`
- `['seek', 123]`
- `['seek-percent', 42]`
- `['set-volume', 70]`
- `['stop']`

The *receiver* may send the following commands to the client, encoded as JSON:

- `['status', {filename, title, album, artist, length, progress, volume, playing}]`

A *receiver* announces itself via [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS), with the following properties:

- service type: `_fasp._tcp.`
- name: a url-safe, ASCII string
- id: a random hex ID, 16 characters
- hostname
- port

## Existing implementations

- [`fasp-server-cli`](https://github.com/derhuerst/fasp-server-cli) – A proof-of-concept *receiver* based on [`mplayer`](http://www.mplayerhq.hu/).
- [`fasp-client-cli`](https://github.com/derhuerst/fasp-client-cli) – A proof-of-concept command line *client*.

## Libraries

- [`fasp-client`](https://github.com/derhuerst/fasp-client) – A JS lib to connect to a *receiver* and send commands. It can also serve local files on demand, for the *receiver* to fetch. [`fasp-client-cli`](https://github.com/derhuerst/fasp-client-cli) uses it.
- [`search-fasp-receivers`](https://github.com/derhuerst/search-fasp-receivers) – Search for *receivers* in the local network.
- [`fasp-audio-receiver`](https://github.com/derhuerst/fasp-audio-receiver) – A JS lib to create & announce a *receiver*. You have to implement the audio playing.
- [`fasp-server`](https://github.com/derhuerst/fasp-server) – A JS lib to run a *receiver*, including audio playing. [`fasp-server-cli`](https://github.com/derhuerst/fasp-server-cli) uses it.
