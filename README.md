oe-rpb-manifest
=================

OE RPB Repo manifest repository with Advantech layer

This repository is based on 96boards/oe-rpb-manifest, and add Advantech add-on features.
For details about original oe-rpb-manifest, you can check the README below.
https://github.com/96boards/oe-rpb-manifest/blob/master/README.md

Repo init
---------

To get the latest version of each meta-layers, you can use default.xml.
```
$ repo init -u https://github.com/ADVANTECH-Corp/oe-rpb-manifest.git
```

To get the release version, you can use a specific xml, e.g. 16.06.xml.
```
$ repo init -u https://github.com/ADVANTECH-Corp/oe-rpb-manifest.git -m 16.06.xml
```

