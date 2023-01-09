
## CREDITS

```
Architecture: aarch64
Maintainer: @termux
Homepage: https://termux.dev

Architecture: aarch64
Maintainer: @ubuntu
Homepage: https://termux.dev
```

### How To Install

```
apt update && apt upgrade && apt install proot-distro build-essential xorg*
```

```
proot-distro install ubuntu
```

```
proot-distro login ubuntu
```
## now install all ubuntu-gnome-dep
```
apt update;apt install ubuntu-desktop nano plank gnome-session-flashback gnome-terminal ubuntu-wallpapers dbus-x11 -y
```
## than clone repo
```
git clone https://github.com/Saikatsaha1996/Ubuntu-Desktop.git && cd Ubuntu-Desktop
```
```
cp vncstart /usr/local/bin/vncstart && chmod +x /usr/local/bin/vncstart
```

```
mkdir $HOME/.vnc && cp xstartup $HOME/.vnc/xstartup && chmod +x $HOME/.vnc/xstartup && cd $HOME && mkdir -p /run/dbus && dbus-daemon --system
```
## then start your ubuntu desktop
```
vncstart
## vncserver will ask for password do yourself

```
## than connect to vnc 

```
localhost:1
## your password
```
