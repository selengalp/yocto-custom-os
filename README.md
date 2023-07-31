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