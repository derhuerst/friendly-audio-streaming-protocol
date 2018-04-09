# Getting Started

## Server

On the machine that is supposed to receive audio, install [`mpv`](https://mpv.io/). On macOS, run this:

```shell
brew install mpv
```

Install the server and give it a name and assign a port:

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

Run this command on any machine that you want to control the audio from.

```shell
npm i -g fasp-client-cli
```

Using the following command, you can let the client search for receivers/servers and pick one.

```shell
fasp-client --pick
```

Once you have picked one, you can just run `fasp-client` and it will try reconnect to the receiver from last time.

**Congrats, you're now set up!**

Having the client running, type `:` and enter a URL of an audio file and press enter. It should start to play shortly after.
