
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
sudo mkdir -p /run/user/$(id -u)
sudo chown $(id -u):$(id -g) /run/user/$(id -u)
export XDG_RUNTIME_DIR=/run/user/$(id -u)

mkdir -p $XDG_RUNTIME_DIR
chmod 700 $XDG_RUNTIME_DIR

export XDG_SESSION_TYPE="x11"
export XDG_SESSION_DESKTOP="gnome"
#export GDMSESSION="ubuntu"
export XDG_CONFIG_DIRS=/etc/xdg
export XDG_CURRENT_DESKTOP=ubuntu:GNOME
export XDG_SESSION_CLASS=user
export XDG_DATA_DIRS=/usr/share/gnome:/usr/local/share/:/usr/share/
gnome-session --disable-acceleration-check &
```
## GNOME INSTALLATION ##
 
```
apt install ubuntu-desktop sudo nano
sudo usermod -aG droidspaces-gpu,sudo,video,audio,input,render,plugdev ubuntu
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
## IMP CMD
```
rm -rf /run/dbus/pid &

sudo service dbus start &
sudo service gdm3 start &
dbus-daemon --system &
dbus-launch --exit-with-session &
gnome-shell --x11 --sm-disable &
LIBGL_ALWAYS_SOFTWARE=1
dbus-run-session -- gnome-session --disable-acceleration-check
```
```
#!/bin/sh
export XDG_RUNTIME_DIR=/run/user/$(id -u)
mkdir -p /run/user/$(id -u)
chmod 700 /run/user/$(id -u)
chown $(id -u):$(id -g) /run/user/$(id -u)
chown $(id -u):$(id -g) /tmp
chmod 1777 /tmp

service dbus start

# UDEV (safe way)
export SYSTEMD_IGNORE_CHROOT=1
#SYSTEMD_IGNORE_CHROOT=1 /lib/systemd/systemd-udevd &
sleep 2
SYSTEMD_IGNORE_CHROOT=1 udevadm trigger &
SYSTEMD_IGNORE_CHROOT=1 udevadm settle &

# SEAT (IMPORTANT FIX)
export LIBSEAT_BACKEND=seatd
export SEATD_VTBOUND=0

seatd -g root &
#sudo -E seatd

# Permissions (temporary but OK)
chmod 777 /dev/input/event*
fuser -k /dev/dri/card0

# Wayland backend
export VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/freedreno_icd.aarch64.json
export SYSTEMD_IGNORE_CHROOT=1
export WLR_BACKENDS=drm,libinput
#export WLR_RENDERER=vulkan
export WLR_DRM_DEVICES=/dev/dri/card0
export WLR_LIBINPUT_NO_DEVICES=1
export WLR_DRM_NO_MODIFIERS=1
#export TU_DEBUG=all
export GDK_BACKEND=wayland
#export XORG_NO_LIBINPUT=1
export TU_DEBUG=noconform
export MESA_LOADER_DRIVER_OVERRIDE=zink
#export XORG_NO_SHADOW_FB=1
export GALLIUM_DRIVER=zink
export ZINK_DESCRIPTORS=lazy

#export KWIN_DRM_NO_MODIFIERS=1
#export KWIN_BACKEND=wayland
#export KWIN_DRM_DEVICES=/dev/dri/card0
#export KWIN_COMPOSE=O2
#export KWIN_OPENGL_INTERFACE=egl
#export WAYLAND_DISPLAY=wayland-0
#export GBM_BACKEND=msm
#export WLR_DRM_NO_ATOMIC=1
#export KWIN_DRM_NO_AMS=1
#export KWIN_DRM_USE_EGL_STREAMS=0
#export KWIN_FORCE_SW_CURSOR=1
#export KWIN_DRM_LEASE=0
#unset DISPLAY
exec sway --unsupported-gpu -d
#startx -- -logverbose 7 -logfile /tmp/xorg.log
#dbus-run-session kwin_wayland
```
## systemd user permission service 
sudo nano /etc/systemd/system/fix-user-perm.service
```
[Unit]
Description=Fix User Run Directory Permissions
After=systemd-user-sessions.service

[Service]
Type=oneshot
#ExecStartPre=/usr/bin/mkdir -p /run/user/1000
ExecStart=-/usr/bin/chown -R 1000:1000 /run/user/1000
ExecStart=-/usr/bin/chmod 700 /run/user/1000
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```
sudo systemctl daemon-reload
sudo systemctl enable fix-user-perm.service
