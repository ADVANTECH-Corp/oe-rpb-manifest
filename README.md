oe-rpb-manifest
=================

OE RPB Repo manifest repository with Advantech layer

This repository is based on [96boards/oe-rpb-manifest](https://github.com/96boards/oe-rpb-manifest), and add Advantech add-on features.
For details about original oe-rpb-manifest, you can check the [README](https://github.com/96boards/oe-rpb-manifest/blob/morty/README.md) file.

BSP Source
----------

Create your own BSP folder first.
```
$ mkdir <BSP folder>
$ cd <BSP folder>
```

To get the latest version of each meta-layers, you can use default.xml.
```
$ repo init -u https://github.com/ADVANTECH-Corp/oe-rpb-manifest.git -b morty
```

To get an official release version, you can assign a specific xml, e.g. 410cLBV1040.xml.
```
$ repo init -u https://github.com/ADVANTECH-Corp/oe-rpb-manifest.git -b morty -m 410cLBV1040.xml
```

Finally, pull down the BSP by running
```
$ repo sync
```

Setup Environment
-----------------

MACHINE values can be:

- rsb-4760
- epc-r4761

DISTRO values can be:

- rpb
- rpb-wayland

```
$ source setup-environment <Your build folder>
```

By default, we adopt **rpb** DISTRO.

Images
------

[meta-rpb](https://github.com/96boards/meta-rpb) provides the following images. Currently, we adopt **rpb-desktop-image** by default.

- rpb-console-image
- rpb-desktop-image
- rpb-minimal-image
- rpb-qt5-image
- rpb-weston-image

To build the image, run
```
$ bitbake rpb-desktop-image
```

To build kernel only, run
```
$ bitbake linux-linaro-qcomlt
```

Deploy
------

### Fastboot

By default, we use `fastboot` utility to flash images into on-board eMMC. On Ubuntu, you can get the package by this way.
```
$ sudo apt-get install android-tools-fastboot
```

To download the images, the target device must be booted into `fastboot mode`.

There are 2 ways to do this.

1. Boot from rescue sdcard

 - Download the rescue image from [here](http://builds.96boards.org/releases/dragonboard410c/linaro/rescue/latest/). It will be named like `dragonboard410c_sdcard_rescue-<version>.zip`.

 - Flash the rescue image into a sdcard. Then, insert the sdcard and boot from it. You will enter the fastboot mode by default.

2. Hold volume down key when booting

 - While holding down volume down key, power on the target device.

 - After a few seconds, release Vol down key. Then, it will enter fastboot mode as well.

 - You can only do this, when bootloader is already flashed on your target device.

Once you enter fastboot mode, you can plug a USB cable from host to target device.
To verify the fastboot connection, you can run:
```
$ sudo fastboot devices
```

### Bootloader

Besides, you also need the Linux bootloader package from [here](http://builds.96boards.org/releases/dragonboard410c/linaro/rescue/latest/) to your development host, it will be named something like `dragonboard410c_bootloader_emmc_linux-<version>.zip`.

Unzip the file and run the `flashall` script to update bootloader.

### Flash into eMMC

At the end of any successful build you will end up with the following artifacts.

 - `IMAGE-MACHINE.ext4.gz`  and
 - `boot-MACHINE.img`

If your IMAGE is `rpb-desktop-image` and MACHINE is `rsb-4760`, the images will be `rpb-desktop-image-rsb-4760.ext4.gz` and `boot-rsb-4760.img` respectively.

You can use fastboot to flash them as well.
```
$ fastboot flash boot boot-MACHINE.img
```

Because fastboot supports sparse image, you have to transform the rootfs image before flashing.
```
$ gunzip IMAGE-MACHINE.ext4.gz
$ ext2simg -v IMAGE-MACHINE.ext4 IMAGE-MACHINE.img
$ fastboot flash rootfs IMAGE-MACHINE.img
```
