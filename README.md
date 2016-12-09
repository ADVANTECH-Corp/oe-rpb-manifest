oe-rpb-manifest
=================

OE RPB Repo manifest repository with Advantech layer

This repository is based on [96boards/oe-rpb-manifest](https://github.com/96boards/oe-rpb-manifest), and add Advantech add-on features.
For details about original oe-rpb-manifest, you can check the [README](https://github.com/96boards/oe-rpb-manifest/blob/krogoth/README.md) file.

BSP Source
----------

Create your own BSP folder first.
```
$ mkdir <BSP folder>
$ cd <BSP folder>
```

To get the latest version of each meta-layers, you can use default.xml.
```
$ repo init -u https://github.com/ADVANTECH-Corp/oe-rpb-manifest.git -b krogoth
```

To get the release version, you can use a specific xml, e.g. 16.09.xml.
```
$ repo init -u https://github.com/ADVANTECH-Corp/oe-rpb-manifest.git -b krogoth -m 16.09.xml
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
