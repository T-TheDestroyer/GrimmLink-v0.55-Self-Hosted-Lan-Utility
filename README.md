# GrimmLink

A private network for you and your friends, as if everyone were on the same
Wi-Fi. Make up a network name and a password, give both to the people you
want to connect with, and press the cat. No account and no server.

It is built for LAN gaming first: a game hosted on one device shows up in the
LAN list on the others. Anything else that works on a local network works
too, such as shared folders.

![The tutorial that opens on first start](docs/tutorial.png)

## Download

Get the latest build from the [Releases page](../../releases).

| System | File | Notes |
| --- | --- | --- |
| Windows 10 and 11 | `GrimmLink-windows.zip` | Unzip, keep the files together, run `GrimmLink.exe`. `README.txt` inside has the details. |
| Android 8 or newer (64-bit) | `GrimmLink.apk` | Allow installing from your browser or file manager when asked. |
| Ubuntu and other Linux | `GrimmLink-ubuntu.tar.gz` | Command line, with an installer for running as a service. `README.txt` inside. |

## Why GrimmLink

- **No sign-in.** There is no account, no email and no login. A network is
  just a name and a password that you make up. Nothing about you or your
  network is registered anywhere.
- **No ads, no tracking.** GrimmLink shows no ads and collects nothing. It
  does not phone home.
- **Self-hosted.** There is no GrimmLink server. Your devices find each
  other and talk to each other directly, so there is no company in the
  middle that can read your traffic, limit you to a number of devices, start
  charging, or shut the service down.
- **Private.** Everything between your devices is encrypted with WireGuard.
  Only someone who knows the network name and the password can join.
- **Free.** All of it, with no paid tier.

The price of having no server in the middle is that GrimmLink depends on
what each person's own network allows. Most home internet works. Some
networks do not. Please read [Limits](#limits-please-read) before you count
on it for something.

## Setting it up

### 1. Install

**Windows.** Unzip `GrimmLink-windows.zip` anywhere and keep the files
together. Run `GrimmLink.exe`.
- If Windows says "Windows protected your PC", click More info, then Run
  anyway. That appears because the program is new and not signed by a big
  publisher.
- Windows asks "Do you want to allow this app to make changes?" every time
  you start it. Answer Yes. Creating a network adapter needs that permission.
- If Windows Firewall asks, click Allow.

**Android.** Open `GrimmLink.apk` on the phone and allow your browser or
file manager to install apps when asked. On first start Android asks to
allow a VPN, and to show notifications. Say yes to both. Only traffic to
GrimmLink's own 100. addresses goes through the VPN; everything else on the
phone is untouched.

**Linux.** Unpack `GrimmLink-ubuntu.tar.gz` and follow the `README.txt`
inside. It is a command-line program with an installer that runs it as a
service.

### 2. Make a network

Press the + button and make up a **network name** and a **password** of 10
or more characters. That is all a network is. It is saved, so you only type
the password once on each device.

### 3. Share it

Give the name and the password to the people you want to connect with.
Everyone types exactly the same two things into their own GrimmLink. Capital
letters count. Anyone who has both can join, so treat the password like a
house key.

### 4. Press the cat

The cat turns from grey to green when you are connected. The other devices
then show up in the list:

- on the same Wi-Fi, within a few seconds;
- over the internet, usually within a minute of them connecting.

Each device gets its own address starting with `100.` that never changes
for that network. Tap any address to copy it.

### 5. Play

A game hosted by anyone in the list should appear in the game's own LAN
list on the other devices. If it does not, copy the host's `100.` address
from GrimmLink and paste it into the game's "direct connect" or "add
server" box.

Some games need a port number after the address. Options has a **Game
port** box for that: put the number in once and every address you copy
comes with it, for example `100.92.196.164:19132`.

Support for games may vary as each game treats LAN connections differently
but I have tested Minecraft Java and Bedrock Editions on PC and Android,
SuperTuxKart on Android, and Rainbow 6 Siege on PC/Steam. Contact me if a
specific game is having trouble and I'll do my best.

## Reading the list

Under each device is how you are connected to it:

| It says | What it means |
| --- | --- |
| **direct**, with a time in ms | Connected straight to that device. This is the normal case and the fastest. |
| **through NAME** | There is no straight path between you and that device, so NAME, who is connected to both of you, passes the traffic along. It works the same, a little slower, and only while NAME stays connected. NAME cannot read it. |
| **connecting…** | The device has been found but cannot be reached yet. If it stays like this, see Limits. |

## Phones on mobile data

A phone on mobile data (not Wi-Fi) usually cannot be connected to from
outside. On its own it will not join a network.

It can join if one PC in the network has a way in from the internet. On
that PC, tick **Open a router port (UPnP)**, under the status line beside
the cat. GrimmLink then asks the home router to send whatever arrives on one
port to that PC, the same as setting up port forwarding by hand. The line
under the box says how it went:

| It says | What it means |
| --- | --- |
| Port 31874 is open | Done. Phones on mobile data can connect to this PC and reach everyone else through it. (The number will differ.) |
| The router did not answer | The router does not do UPnP, or it is switched off in the router's settings. |
| The router refused | It does UPnP but said no. |
| Open, but not reachable from outside | The router opened the port, but your internet provider shares one public address between customers, so nothing can reach it. |

One PC with an open port is enough for the whole network, and it has to be
connected for the phone to get in. The port is closed again when you
disconnect.

## Limits (please read)

GrimmLink has no server to fall back on, so it can only do what the
networks involved allow. It will not work for everyone. These are the
situations I know of:

- **Your internet provider decides a lot.** Some providers put many
  customers behind one shared public address (often called CGNAT). This is
  common on mobile data, satellite, and some fibre and cable plans. Devices
  on such a connection often cannot be reached directly, and opening a
  router port does not help, because the block is at the provider, not at
  your router. I cannot fix this from inside the app.
- **Not every router does UPnP.** Some do not support it, some ship with it
  switched off, and some people turn it off on purpose. If "Open a router
  port" says the router did not answer or refused, you can switch UPnP on in
  the router's settings or set up port forwarding by hand, if you have
  access to the router. On a shared, rented or locked-down router you may
  not.
- **School, work, hotel and public Wi-Fi often block it.** GrimmLink needs
  UDP traffic and uses the public BitTorrent network to find devices. Many
  managed networks block one or both. On those it may find nobody, or only
  devices on the same Wi-Fi.
- **It can look like BitTorrent to your provider.** GrimmLink uses that
  network only as a meeting place; nothing is downloaded or shared. A
  provider that blocks or slows BitTorrent may still interfere with finding
  devices. You can turn this off in Options, which leaves the local network
  only.
- **"through NAME" depends on NAME.** When two devices can only talk
  through a third, that third device has to stay connected, and its upload
  speed is the limit. If it disconnects, so do they.
- **Finding people is not instant.** With no server keeping a list, the
  first device from another home can take up to about a minute to appear.
- **Games differ.** Some games only look for LAN servers in ways GrimmLink
  does not carry yet, and some refuse addresses that do not look like a
  home network. Copying the address in by hand works more often than the
  LAN list. Console games and anything that needs the console itself to be
  on the network will not work, since consoles cannot run GrimmLink.
- **Speed is your own connection's.** Traffic goes between your homes, not
  through a data centre. Latency and speed are whatever the slower of the
  two connections gives.
- **No iPhone or Mac version** yet.

**Before you rely on it,** have everyone run **Options, Network check**. It
takes about 15 seconds, changes nothing, and says in plain words whether
that network allows direct connections, whether devices can be found over
the internet, and whether the router will open a port. If the check says a
network is blocked, GrimmLink will most likely not work there, and that is
the network's doing rather than something a setting can fix.

GrimmLink is free and comes with no guarantee. I would rather you know all
this up front than find out halfway through setting up a game night.

## If nobody shows up

1. Check that everyone typed exactly the same network name and password.
2. Check that everyone is on the same version (shown at the bottom of
   Options).
3. Have each person run Options, Network check, and compare the results
   with Limits above.
4. If it still fails, use Options, Copy log on the device that is missing
   the others and send it to me.

## How it works, briefly

- Devices find each other with nothing in the middle: by broadcast on the
  same Wi-Fi, and through the public BitTorrent network across the internet.
- They connect directly whenever their routers allow it.
- Devices introduce each other, so one connection into a network brings in
  everyone, and a device connected to two others can pass traffic between
  them when they cannot connect directly.
- The "is anyone hosting?" announcements games send are carried to every
  device, which is what fills in LAN lists.

## Support

GrimmLink is free. If you like what I am doing here, you can
[buy me a coffee](https://buymeacoffee.com/grimmcreations) or
[support me on Patreon](https://www.patreon.com/c/GrimmCreations).

## Licence

Free to use and to pass on unchanged. Not to be modified or sold. The full
terms are in [LICENSE](LICENSE). [CHANGELOG.txt](CHANGELOG.txt) lists what
changed in each version.

## Credits

Built on [WireGuard](https://www.wireguard.com/) through wireguard-go and, on
Windows, the Wintun driver (licences in the [licenses](licenses) folder). "WireGuard"
and "Wintun" are trademarks of their owners; GrimmLink is not affiliated with
or endorsed by them.
