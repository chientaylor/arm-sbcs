# Radxa R5S

## Specifications

- RK3588 (4 A76, 4 A55 cores) for 64-bit OS Support
- 2.5 Gb Ethernet
- Up to 16 GB RAM
- M.2 M-Key
- USB-C Power
- 2x USB 3.0 Plugs
- 2x HDMI-out Plug
- 1x HDMI-in Plug

## First Impressions

Specs Ordered

- 16 GB RAM

## Review

https://tchien.com/2022/12/22/radxa-rock5b

## 3D Models

One thing I have to give Radxa credit for is providing a full 3D model of the device. I used this to make a [case](https://www.printables.com/model/345623-radxa-rock5b-case-for-cooler) and [heatsink adapter](https://www.printables.com/model/345229-radxa-rock-5b-ice-tower-low-profile-conversion-bra) for the SBC.

https://wiki.radxa.com/Rock5/hardware

## Gotchas

2022-12-22

The board is incredibly picky about its choice of microSD card. None of my Sandisk cards worked at all, either in 16, 32, or 128 GB variants. In the end, my Samsung endurance and performance SD cards worked. I haven’t been able to test an NVME SSD or an eMMC yet.

Another issue is that when connected to the Steam Deck’s USB C charger, the board will start to boot, and then hard reset. Whether this is because of the Steam Deck’s implementation of PD, I don’t know, but I have to wait for USB C to C cables to test a proper charger.

## OS Support

### Radxa-provided OSes

These images are provided by Radxa directly, so should have the best compatibility.

https://wiki.radxa.com/Rock5/downloads

#### Debian Bullseye (XFCE4)

2022-12-22

Radxa provides a Desktop Debian image, and it boots as expected. It does have an issue where the apt GPG key for Radxa’s OS libraries is not pre-installed. It also defaults to using network-manager through the GUI, which is fine, since this is a desktop image. However, they have no server image for Debian.

Another issue that I had repeatedly was that performing an apt upgrade would sometimes just break the OS on reboot. It would lock up just before the lightdm initialized, which makes me think something from that broken apt repo was necessary for this to work right.

#### Ubuntu Focal (Server)

2022-12-22

The Ubuntu image was… odd. It’s Ubuntu 20.04, but it seems to be missing most of the network management features, defaulting to network-manager. Whatever they did to the Focal image, they had stripped so much away that it could barely be called Ubuntu at that point, which was a problem for my Ansible playbooks.

#### Android 12

2022-12-22

I could not get this to start, no matter what I used. Sometimes it would get to the initialization screen, and then crash. I tried all of my microSD cards, and none of them changed the boot looping. Eventually I gave up and moved on.

### Armbian

https://www.armbian.com/rock-5b/

#### Bullseye Server

2022-12-22

Armbian is a solid offering. The initial ssh in as root with the default password will prompt you to change the root password and set up your user. This is a fairly good idea, since it avoids having a default user on the OS. After this is done, the OS is somewhat clean, except for the Armbian APT repo.

### DietPi

https://dietpi.com/downloads/images/DietPi_ROCK5B-ARMv8-Bullseye.7z

2022-12-23

I’m really starting to enjoy the DietPi system, as it makes automating an installation extremely straightforward. It also covers all the SBCs I care about, so I can deploy the same OS to all my SBCs.

For the Rock5B, the only issue I had was with the same SD card pickiness as before. I didn’t see anything hugely concerning or different during startup. Overall, this might actually be something I stick with, even though I’m not a huge fan of all the overhead.
