# NanoPi R5S

## Specifications

- RK3568B2 (4 A55 cores) for 64-bit OS Support
- 2x 2.5 Gb Ethernet
- 1x Gb Ethernet
- Up to 4 GB RAM
- Mali G52 GPU
- M.2 M-Key
- USB-C Power
- 2x USB 3.0 Plugs
- 1x HDMI Plug

## First Impressions

Specs Ordered

- 4 GB RAM
- No MAC Address Chip
- Metal Case

### Case
The Metal case is solid and very hefty, with all four screws exposed on the bottom plate. This exposes the M.2 slot directly. The case is then secured to the board with four much smaller screws. All screws are magnetic and black to match the board.

However, the case does not seem to be easily removable. Between whatever thermal mechanism exists between the case and the CPU, the front LED plastic channels, and the rear Ethernet ports, it is difficult to remove the board without excessive force.

There is also no indication of which direction the baseplate should go, because it is directional, but only because of about one millimeter of clearance on some board components.

## Review

https://tchien.com/2022/12/22/friendlyarmfriendlyelec-nanopi-r5s

## OS Issues

### Debian 10 (FriendlyARM Source)

The provided version of Debian 10 has some very odd choices. It seems to want to be a desktop, with X, Wayland, and LXDE installed by default. It also has some packages held back, although none are system critical, and all of them seem related to the UI.

I decided that, since I'm not going to use the UI, I would see what happened when I upgraded the packages. I found all the held packages with `apt-mark showhold`, then replaced all the newlines (`\n`) with spaces, and then used that list to unhold all the packages at once.

```
apt-mark unhold chromium-x11 chromium-x11-dbgsym dvb-tools-dbgsym ffmpeg ffmpeg-dbgsym gir1.2-gst-plugins-bad-1.0 gir1.2-gst-plugins-base-1.0 glmark2-data glmark2-es2-x11 glmark2-es2-x11-dbgsym gstreamer1.0-gl gstreamer1.0-libav gstreamer1.0-libav-dbg gstreamer1.0-plugins-bad gstreamer1.0-plugins-bad-dbg gstreamer1.0-plugins-bad-doc gstreamer1.0-plugins-base gstreamer1.0-plugins-base-dbg gstreamer1.0-plugins-base-doc gstreamer1.0-plugins-good gstreamer1.0-plugins-good-dbg gstreamer1.0-plugins-good-doc gstreamer1.0-plugins-ugly gstreamer1.0-plugins-ugly-dbg gstreamer1.0-plugins-ugly-doc gstreamer1.0-rockchip1 gstreamer1.0-rockchip1-dbgsym gstreamer1.0-tools gstreamer1.0-x ir-keytable-dbgsym libavcodec-dev libavcodec58 libavcodec58-dbgsym libavdevice-dev libavdevice58 libavdevice58-dbgsym libavfilter-dev libavfilter7 libavfilter7-dbgsym libavformat-dev libavformat58 libavformat58-dbgsym libavresample-dev libavresample4 libavresample4-dbgsym libavutil-dev libavutil56 libavutil56-dbgsym libdrm-common libdrm-cursor libdrm-cursor-dbgsym libdrm-cursor-dev libdrm-dev libdrm2 libdrm2-dbgsym libdvbv5-0-dbgsym libfile-listing-perl libgstreamer-gl1.0-0 libgstreamer-plugins-bad1.0-0 libgstreamer-plugins-bad1.0-dev libgstreamer-plugins-base1.0-0 libgstreamer-plugins-base1.0-dev libgstreamer1.0-0 libgstreamer1.0-0-dbg libkms1 libkms1-dbgsym libmpv1 libmpv1-dbgsym libpostproc-dev libpostproc55 libpostproc55-dbgsym libpulse-mainloop-glib0 libpulse0 libpulsedsp librockchip-mpp-dev librockchip-mpp1 librockchip-mpp1-dbgsym librockchip-vpu0 librockchip-vpu0-dbgsym libswresample-dev libswresample3 libswresample3-dbgsym libswscale-dev libswscale5 libswscale5-dbgsym libv4l-0 libv4l-0-dbgsym libv4l-dev libv4l-rkmpp libv4l-rkmpp-dbgsym libv4l2rds0-dbgsym libv4lconvert0-dbgsym mpv mpv-dbgsym openbox openbox-dev pulseaudio pulseaudio-utils qv4l2-dbgsym rkisp-engine rktoolkit rktoolkit-dbgsym rkwifibt-broadcom-firmware rkwifibt-dev-tools rkwifibt-dev-tools-dbgsym rockchip-mpp-demos rockchip-mpp-demos-dbgsym v4l-utils v4l-utils-dbgsym xdmx xdmx-dbgsym xdmx-tools xdmx-tools-dbgsym xnest xnest-dbgsym xorg-server-source xserver-common xserver-xephyr xserver-xephyr-dbgsym xserver-xorg-core xserver-xorg-core-dbgsym xserver-xorg-dev xserver-xorg-legacy xserver-xorg-legacy-dbgsym xvfb xvfb-dbgsym xwayland xwayland-dbgsym

apt full-upgrade -y
```

The upgrade process removed quite a few packages, all `-dbgsym`, the Debug Symbol packages. Because the UI is auto-logged in, similar to a Raspberry Pi, I also spent some time removing that.

```
apt purge -y chromium-x11 ffmpeg xwayland xserver-common pulseaudio openbox gstreamer1.0* lxde xnest lightdm
apt autoremove --purge -y
```

I then killed all Pi's user processes and deleted the user.

```
killall -u pi
deluser pi
rm -rf /home/pi
```
