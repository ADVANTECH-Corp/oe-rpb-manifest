oe-rpb-manifest
=================

OE RPB Repo manifest repository with Advantech layer

This repository is based on [96boards/oe-rpb-manifest](https://github.com/96boards/oe-rpb-manifest), and add Advantech add-on features.
For details about original oe-rpb-manifest, you can check the [README](https://github.com/96boards/oe-rpb-manifest/blob/jethro/README.md) file.

Repo init
---------

To get the latest version of each meta-layers, you can use default.xml.
```
$ repo init -u https://github.com/ADVANTECH-Corp/oe-rpb-manifest.git
```

To get the release version, you can use a specific xml, e.g. 16.09.xml.
```
$ repo init -u https://github.com/ADVANTECH-Corp/oe-rpb-manifest.git -b krogoth -m 16.09.xml
```

