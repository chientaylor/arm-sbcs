# StarFive VisionFive 2

## Specifications

- JH7110 quad-core RISC-V
- 8 GB LPDDR4 RAM
- 2x 1 Gb Ethernet (with MAC chips!)
- GPIO
- PoE with HAT
- 2x USB 3.0, 2x USB 2.0
- DSI, CSI, MIPI Connectors
- HDMI 2.0

## Review

Coming Soon (tm)

## Gotchas

- Cares very deeply about the SD cards you can use
- Barely any compatibility
- Board has components very close to the mounting holes making creating a case very challenging

## OS Support

There is a massive caveat here; right now my boards are split between those I upgraded the flash on, and those I didn't. Those I did upgrade the flash on are not working with some images. Those I didn't are not working with some images. There seems to be no overlap and no compatibility between the two. For now, I'll ignore the issue as a teething problem, but it's very frustrating in the meantime.

Another issue is that there appears to be two different variations of the NOR flash. One has the uboot section on `/dev/mtd2` [Link](https://doc-en.rvspace.org/VisionFive2/Quick_Start_Guide/VisionFive2_SDK_QSG/spl_new.html#updating_spl_and_u_boot-vf2__section_zpj_cqt_yvb), while another has it at /dev/mtd1 [Section 4.4](https://rvspace.org/en/project/VisionFive2_Debian_User_Guide)

### Provided Debian

SD Mode, Upgraded firmware

Works, but only just. No `apt upgrade` due to custom packages. based on a version of Sid that has been deprecated.

### DietPi

Stock flash only

Kind of works but it's based on Debian Sid, so not exactly stable.

### Ubuntu

Stock flash only

Based on Ubuntu 23.04, so not sn LTS image.

### Armbian

Nothing

I couldn't get this to boot at all.