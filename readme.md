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
- `['remove', 2]`
- `['stop']`
- `['resume']`
- `['pause']`
- `['seek', 123, false, false]` (relative, in seconds)
- `['seek', 123, true, false]` (absolute, in seconds)
- `['seek', 123, true, true]` (absolute, in percent)
- `['seek', 123, false, true]` (relative, in percent)
- `['set-volume', 70]`
- `['get-props']`

The *receiver* may send the following commands to the client, encoded as JSON:

- `['prop', {filename, title, album, artist, length, progress, volume, playing}]`
- `['prop', 'filename', 'some-file.ogg']`
- `['prop', 'path', 'path/to/some-file.ogg']`
- `['prop', 'duration', 219.5]`
- `['prop', 'percent-pos', 2,477]`
- `['prop', 'time-pos', 54.5]`
- `['prop', 'pause', false]`
- `['prop', 'volume', 70]`
- `['prop', 'metadata', {title, album, artist, album_artist, track, disc}]`
- `['prop', 'artwork', 'https://example.org/path/to/artwork.jpg']`

A *receiver* announces itself via [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS), with the following properties:

- service type: `_fasp._tcp.`
- `name`: a url-safe, ASCII string
- `id`: a random hex ID, 16 characters
- `version`: the version of the protocol, `2` currently
- hostname
- port

## Existing implementations

- [`fasp-server-cli`](https://github.com/derhuerst/fasp-server-cli) – A proof-of-concept *receiver* based on [`mpv`](https://mpv.io/).
- [`fasp-client-cli`](https://github.com/derhuerst/fasp-client-cli) – A proof-of-concept command line *client*.
- [`fasp-web-client`](https://github.com/derhuerst/fasp-client-cli) – A proof-of-concept *client* web app.

## Libraries

- [`fasp-client`](https://github.com/derhuerst/fasp-client) – A JS lib to connect to a *receiver* and send commands. It can also serve local files on demand, for the *receiver* to fetch. [`fasp-client-cli`](https://github.com/derhuerst/fasp-client-cli) and [`fasp-web-client`](https://github.com/derhuerst/fasp-web-client) use it.
- [`search-fasp-receivers`](https://github.com/derhuerst/search-fasp-receivers) – Search for *receivers* in the local network.
- [`fasp-receiver`](https://github.com/derhuerst/fasp-receiver) – A JS lib to create & announce a *receiver*. You have to implement the audio playing.
- [`fasp-server`](https://github.com/derhuerst/fasp-server) – A JS lib to run a *receiver*, including audio playing. [`fasp-server-cli`](https://github.com/derhuerst/fasp-server-cli) uses it.
