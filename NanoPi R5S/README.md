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

### Operating Systems
The intended use case for this device is as an internet gateway, using FriendlyWRT, their Docker-enabled version, or a Ubuntu Core derivitive. It's fine, but it's one of those weird Chinese images that has too much random stuff on it for me to trust, especially since the source is Google Drive.

It's not a bad port of OpenWRT, but I would prefer is that they contribute their changes directly to OpenWRT as well as make their own OS. The R4S has an image in Snapshot, but not the R5S.

The good thing is that all of these seem to be very up-to-date. The version of Debian available is Buster, but it was built June 30th, the day before I started testing. The rest were at least all built in June, so that makes testing easier.

The FriendlyWRT image was the one I was interested in though, so that was the first test. The .img file flashed easily enough, and the bootup was simple. OpenWRT's web interface came up the same as always, and the fact that the interface names silkscreened on the back matched up to how they were marked in the OS was a nice bonus.

## Current OS Support Links

FriendlyELEC Wiki Page: https://wiki.friendlyelec.com/wiki/index.php/NanoPi_R5S#Install_OS

DietPi: https://dietpi.com/downloads/images/DietPi_NanoPiR5S-ARMv8-Bullseye.7z

## Hardware Tree

### USB
```
root@FriendlyWrt:~# uname -a
Linux FriendlyWrt 5.10.110 #1 SMP Tue Jun 21 18:45:08 CST 2022 aarch64 GNU/Linux
root@FriendlyWrt:~# lsusb -tvv
/:  Bus 08.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    ID 1d6b:0003
    /sys/bus/usb/devices/usb8  /dev/bus/usb/008/001
/:  Bus 07.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    ID 1d6b:0002
    /sys/bus/usb/devices/usb7  /dev/bus/usb/007/001
/:  Bus 06.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 5000M
    ID 1d6b:0003
    /sys/bus/usb/devices/usb6  /dev/bus/usb/006/001
/:  Bus 05.Port 1: Dev 1, Class=root_hub, Driver=xhci-hcd/1p, 480M
    ID 1d6b:0002
    /sys/bus/usb/devices/usb5  /dev/bus/usb/005/001
/:  Bus 04.Port 1: Dev 1, Class=root_hub, Driver=ohci-platform/1p, 12M
    ID 1d6b:0001
    /sys/bus/usb/devices/usb4  /dev/bus/usb/004/001
/:  Bus 03.Port 1: Dev 1, Class=root_hub, Driver=ohci-platform/1p, 12M
    ID 1d6b:0001
    /sys/bus/usb/devices/usb3  /dev/bus/usb/003/001
/:  Bus 02.Port 1: Dev 1, Class=root_hub, Driver=ehci-platform/1p, 480M
    ID 1d6b:0002
    /sys/bus/usb/devices/usb2  /dev/bus/usb/002/001
/:  Bus 01.Port 1: Dev 1, Class=root_hub, Driver=ehci-platform/1p, 480M
    ID 1d6b:0002
    /sys/bus/usb/devices/usb1  /dev/bus/usb/001/001
```

### PCI
```
root@FriendlyWrt:~# uname -a
Linux FriendlyWrt 5.10.110 #1 SMP Tue Jun 21 18:45:08 CST 2022 aarch64 GNU/Linux
root@FriendlyWrt:~# lspci -v
0000:00:00.0 PCI bridge: Rockchip Electronics Co., Ltd RK3568 Remote Signal Processor (rev 01) (prog-if 00 [Normal decode])
        Device tree node: /sys/firmware/devicetree/base/pcie@fe260000/pcie@00
        Flags: bus master, fast devsel, latency 0, IRQ 86
        Bus: primary=00, secondary=01, subordinate=ff, sec-latency=0
        I/O behind bridge: 00001000-00001fff [size=4K]
        Memory behind bridge: f4200000-f42fffff [size=1M]
        Prefetchable memory behind bridge: [disabled]
        Expansion ROM at f4300000 [virtual] [disabled] [size=64K]
        Capabilities: [40] Power Management version 3
        Capabilities: [50] MSI: Enable+ Count=1/32 Maskable- 64bit+
        Capabilities: [70] Express Root Port (Slot-), MSI 00
        Capabilities: [b0] MSI-X: Enable- Count=1 Masked-
        Capabilities: [100] Advanced Error Reporting
        Capabilities: [148] Secondary PCI Express
        Capabilities: [160] L1 PM Substates
        Capabilities: [170] Vendor Specific Information: ID=0002 Rev=4 Len=100 <?>
        Kernel driver in use: pcieport
lspci: Unable to load libkmod resources: error -12

0000:01:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller (rev 05)
        Subsystem: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller
        Device tree node: /sys/firmware/devicetree/base/pcie@fe260000/pcie@00/pcie@01,0
        Flags: bus master, fast devsel, latency 0, IRQ 85
        I/O ports at 1000 [size=256]
        Memory at f4200000 (64-bit, non-prefetchable) [size=64K]
        Memory at f4210000 (64-bit, non-prefetchable) [size=16K]
        Capabilities: [40] Power Management version 3
        Capabilities: [50] MSI: Enable- Count=1/1 Maskable+ 64bit+
        Capabilities: [70] Express Endpoint, MSI 01
        Capabilities: [b0] MSI-X: Enable+ Count=32 Masked-
        Capabilities: [d0] Vital Product Data
        Capabilities: [100] Advanced Error Reporting
        Capabilities: [148] Virtual Channel
        Capabilities: [168] Device Serial Number 00-00-00-00-00-00-00-00
        Capabilities: [178] Transaction Processing Hints
        Capabilities: [204] Latency Tolerance Reporting
        Capabilities: [20c] L1 PM Substates
        Capabilities: [21c] Vendor Specific Information: ID=0002 Rev=4 Len=100 <?>
        Kernel driver in use: r8125

0001:10:00.0 PCI bridge: Rockchip Electronics Co., Ltd RK3568 Remote Signal Processor (rev 01) (prog-if 00 [Normal decode])
        Device tree node: /sys/firmware/devicetree/base/pcie@fe270000/pcie@10
        Flags: bus master, fast devsel, latency 0, IRQ 113
        Bus: primary=10, secondary=11, subordinate=11, sec-latency=0
        I/O behind bridge: 00000000-00000fff [size=4K]
        Memory behind bridge: f2200000-f22fffff [size=1M]
        Prefetchable memory behind bridge: [disabled]
        Expansion ROM at f2300000 [virtual] [disabled] [size=64K]
        Capabilities: [40] Power Management version 3
        Capabilities: [50] MSI: Enable+ Count=16/32 Maskable- 64bit+
        Capabilities: [70] Express Root Port (Slot-), MSI 08
        Capabilities: [b0] MSI-X: Enable- Count=128 Masked-
        Capabilities: [100] Advanced Error Reporting
        Capabilities: [148] Secondary PCI Express
        Capabilities: [160] L1 PM Substates
        Capabilities: [170] Vendor Specific Information: ID=0002 Rev=4 Len=100 <?>
        Kernel driver in use: pcieport

0001:11:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller (rev 05)
        Subsystem: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller
        Device tree node: /sys/firmware/devicetree/base/pcie@fe270000/pcie@10/pcie@10,0
        Flags: bus master, fast devsel, latency 0, IRQ 112
        I/O ports at 200000 [size=256]
        Memory at f2200000 (64-bit, non-prefetchable) [size=64K]
        Memory at f2210000 (64-bit, non-prefetchable) [size=16K]
        Capabilities: [40] Power Management version 3
        Capabilities: [50] MSI: Enable- Count=1/1 Maskable+ 64bit+
        Capabilities: [70] Express Endpoint, MSI 01
        Capabilities: [b0] MSI-X: Enable+ Count=32 Masked-
        Capabilities: [d0] Vital Product Data
        Capabilities: [100] Advanced Error Reporting
        Capabilities: [148] Virtual Channel
        Capabilities: [168] Device Serial Number 00-00-00-00-00-00-00-00
        Capabilities: [178] Transaction Processing Hints
        Capabilities: [204] Latency Tolerance Reporting
        Capabilities: [20c] L1 PM Substates
        Capabilities: [21c] Vendor Specific Information: ID=0002 Rev=4 Len=100 <?>
        Kernel driver in use: r8125
```

### CPU Info
```
root@FriendlyWrt:~# cat /proc/cpuinfo
processor       : 0
BogoMIPS        : 48.00
Features        : fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm lrcpc dcpop asimddp
CPU implementer : 0x41
CPU architecture: 8
CPU variant     : 0x2
CPU part        : 0xd05
CPU revision    : 0

processor       : 1
BogoMIPS        : 48.00
Features        : fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm lrcpc dcpop asimddp
CPU implementer : 0x41
CPU architecture: 8
CPU variant     : 0x2
CPU part        : 0xd05
CPU revision    : 0

processor       : 2
BogoMIPS        : 48.00
Features        : fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm lrcpc dcpop asimddp
CPU implementer : 0x41
CPU architecture: 8
CPU variant     : 0x2
CPU part        : 0xd05
CPU revision    : 0

processor       : 3
BogoMIPS        : 48.00
Features        : fp asimd evtstrm aes pmull sha1 sha2 crc32 atomics fphp asimdhp cpuid asimdrdm lrcpc dcpop asimddp
CPU implementer : 0x41
CPU architecture: 8
CPU variant     : 0x2
CPU part        : 0xd05
CPU revision    : 0
```

### Memory Info
```
root@FriendlyWrt:~# cat /proc/meminfo
MemTotal:        3996276 kB
MemFree:         3665220 kB
MemAvailable:    3794696 kB
Buffers:            7460 kB
Cached:           168276 kB
SwapCached:            0 kB
Active:            47896 kB
Inactive:         150152 kB
Active(anon):       5516 kB
Inactive(anon):    40816 kB
Active(file):      42380 kB
Inactive(file):   109336 kB
Unevictable:           4 kB
Mlocked:               0 kB
SwapTotal:             0 kB
SwapFree:              0 kB
Dirty:                 0 kB
Writeback:             0 kB
AnonPages:         22348 kB
Mapped:            27536 kB
Shmem:             24048 kB
KReclaimable:      43972 kB
Slab:              84116 kB
SReclaimable:      43972 kB
SUnreclaim:        40144 kB
KernelStack:        2688 kB
PageTables:         1420 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:     1998136 kB
Committed_AS:      83036 kB
VmallocTotal:   135290159040 kB
VmallocUsed:       21560 kB
VmallocChunk:          0 kB
Percpu:              944 kB
AnonHugePages:         0 kB
ShmemHugePages:        0 kB
ShmemPmdMapped:        0 kB
FileHugePages:         0 kB
FilePmdMapped:         0 kB
CmaTotal:           8192 kB
CmaFree:            2232 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
Hugetlb:               0 kB
```

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
