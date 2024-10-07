# meta-archery-timer

This README file contains information on the contents of the meta-archery-timer layer.

Please see the corresponding sections below for details.

## Quick Start

In an empty directory, clone the Yocto poky distribution, along with this layer:
```
git clone git@git.yoctoproject.org/poky
git clone git@github.com:agherzan/meta-raspberrypi.git
git clone git@github.com:steveicarus/meta-archery-timer.git
```

The result should be a directory with the meta-archery-timer, meta-raspberrypi, and
poky directories.

Next, create a build environment like this:
```
source oe-init-build-env
```

This will create the build directory, and in particular the build/conf directory with
the bblayers.conf and local.conf files. We'll get to those in a second.

Add the meta-archery-timer layer to the stack like this:
```
bitbake-layer add-layer ../meta-raspberrypi
bitbake-layer add-layer ../meta-archery-timer
```
This finishes up the contents of the bblayers.conf file, which should now look like this:
```
# POKY_BBLAYERS_CONF_VERSION is increased each time build/conf/bblayers.conf
# changes incompatibly
POKY_BBLAYERS_CONF_VERSION = "2"

BBPATH = "${TOPDIR}"
BBFILES ?= ""

BBLAYERS ?= " \
  /home/steve/icarus/embedded-archery-timer/poky/meta \
  /home/steve/icarus/embedded-archery-timer/poky/meta-poky \
  /home/steve/icarus/embedded-archery-timer/poky/meta-yocto-bsp \
  /home/steve/icarus/embedded-archery-timer/meta-raspberrypi \
  /home/steve/icarus/embedded-archery-timer/meta-archery-timer \
  "
```

Next, edit the conf/local.conf file and adjust the MACHINE and DISTRO settings:
```
[...]
MACHINE ?= "rpi-archery-timer"
[...]
DISTRO ?= "archery-timer"
```

Now you are ready to build. Do so with this command:
```
bitbake core-image-base
```
The "core-image-minimal" image also works.

The resulting sdimg file is the sdcard image that can be loaded onto an sdcard using
the "Pi Imager" tool. Load that into the sdcard, install it on your raspberry Pi, and
it will boot.

## Dependencies

  URI: git://git.yoctoproject.org/poky
  branch: master

  URI: git@github.com:agherzan/meta-raspberrypi.git
  branch: master

