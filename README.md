# Yocto Test Custom OS

An example repository for developing yocto project by using github submodules and oe layers.
This repository uses `kirkstone` branch of poky.

# Prerequisites

Install the following packages to your system. It is tested on Ubuntu 20.04 LTS.

```
sudo apt install gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev python3-subunit mesa-common-dev zstd liblz4-tool file locales l4z
```

# Compile a minimal image for qemux86
Compile a minimal image for qemux86 by using the following commands:

```
cd poky
source oe-init-build-env ../BUILD
bitbake core-image-minimal
```

Image will be generated under `tmp/deploy/images/qemux86/core-image-minimal-qemux86.ext4`.


# Example of bblayers.conf

```
BBLAYERS ?= " \
  /home/selengalp/yocto-test_custom-os/poky/meta \
  /home/selengalp/yocto-test_custom-os/poky/meta-poky \
  /home/selengalp/yocto-test_custom-os/poky/meta-yocto-bsp \
  /home/selengalp/yocto-test_custom-os/meta-raspberrypi \
  /home/selengalp/yocto-test_custom-os/meta-openembedded/meta-oe \
  /home/selengalp/yocto-test_custom-os/meta-openembedded/meta-multimedia \
  /home/selengalp/yocto-test_custom-os/meta-openembedded/meta-networking \
  /home/selengalp/yocto-test_custom-os/meta-openembedded/meta-python \
  /home/selengalp/yocto-test_custom-os/meta-openembedded/meta-filesystems \
  /home/selengalp/yocto-test_custom-os/meta-virtualization \
  "
```

# Example of local.conf 
Add the end of the conf/local.conf file.

```
# We need to set the default machine ourselves
MACHINE = "raspberrypi4-64"

# We need to set the default distro ourselves
DISTRO = "poky"

# We need to set package type ourselves
PACKAGE_CLASSES ?= "package_ipk"
IMAGE_FEATURES += "package-management"

# We need to set the default distro features ourselves
DISTRO_FEATURES:append = " systemd"

# We need to set the default init manager ourselves
VIRTUAL-RUNTIME_init_manager = "systemd"

# We need to add required packages ourselves
# Add k3s and other requirements as a kubernates distribution
IMAGE_INSTALL:append = " virtualization k3s"
IMAGE_INSTALL:append = " nano git networkmanager openssh sudo"

# We need to set the IMAGE_FSTYPES ourselves
IMAGE_FSTYPES = "rpi-sdimg.gz"
```
