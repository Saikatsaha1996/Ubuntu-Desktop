
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
## GNOME SESSION STARTER ##
```
#for /tmp permession issue do "sudo chmod 1777 /tmp/.ICE-unix" & "sudo chown root:root /tmp/.ICE-unix"
 
export DISPLAY=:0
export PULSE_SERVER=tcp:127.0.0.1:4713
export XDG_RUNTIME_DIR=/tmp
export XDG_SESSION_TYPE="x11"
export XDG_SESSION_DESKTOP="gnome"
export GDMSESSION="ubuntu"
export XDG_CONFIG_DIRS=/etc/xdg
export XDG_CURRENT_DESKTOP=GNOME
export XDG_DATA_DIRS=/usr/share/gnome:/usr/local/share/:/usr/share/
gnome-session --disable-acceleration-check &
```
## GNOME INSTALLATION ##
 
```
apt install ubuntu-desktop sudo nano
```
## DISABLE SNAP ##
 
```
apt-get autopurge snapd
 
cat <<EOF | sudo tee /etc/apt/preferences.d/nosnap.pref
# To prevent repository packages from triggering the installation of Snap,
# this file forbids snapd from being installed by APT.
# For more information: https://linuxmint-user-guide.readthedocs.io/en/latest/snap.html
Package: snapd
Pin: release a=*
Pin-Priority: -10
EOF
```
## FIX SESSION STARTUP ##
```
for file in $(find /usr -type f -iname "*login1*"); do rm -rf $file
   done
```
## FIX SETTINGS ##
```
rm -rvf .config/dconf/user
```
