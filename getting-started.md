# Getting Started

## Server

### Prerequisites

On the machine that is supposed to receive audio, install [`mpv`](https://mpv.io/). Refer to their [installation page](https://mpv.io/installation/) for further details.

```shell
# macOS
brew install mpv
# Ubuntu or similar
sudo add-apt-repository ppa:mc3man/mpv-tests
sudo apt update
sudo apt install mpv
```

On many Linux systems, you also need the `dns_sd.h` headers for [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS):

```js
# Ubuntu or similar
sudo apt install libavahi-compat-libdnssd-dev
```

### Installation

Now, install the server and give it a name and assign a port:

```shell
npm i -g fasp-server-cli
fasp-server <some-name> <port>
```

You can now run the server. It should report something like "… listening on port …".

```
fasp-server
```

You should now be able to control the server using any client in the local network. We will proceed with how to install the command line client.

## Client

Install the client on any machine that you want to control the audio from:

```shell
npm i -g fasp-client-cli
```

On many Linux systems, you also need the `dns_sd.h` headers for [mDNS](https://en.wikipedia.org/wiki/Multicast_DNS):

```js
# Ubuntu or similar
sudo apt install libavahi-compat-libdnssd-dev
```

Using the following command, you can let the client search for receivers/servers and pick one.

```shell
fasp-client --scan
```

It will remember your choice so that you can just run `fasp-client` next time.

**Congrats, you're now set up!**

Having the client running, type `:` and enter a URL of an audio file and press enter. It should start to play shortly after.
