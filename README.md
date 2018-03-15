# Kernel
## Getting the source
```
$ git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git
$ cd linux-stable
$ git checkout v4.15.0-rc9
```
See my current kernel version
```
$ make ARCH=arm kernelversion
```
See my current kernel release
```
$ make ARCH=arm kernelrelease
```

## Build a kernel for QEMU
```
$ cd linux-stable
$ make ARCH=arm CROSS_COMPILE=arm-unknow-linux-gnueabi- mrproper
$ make ARCH=arm versatile_defconfig
$ make ARCH=arm CROSS_COMPILE=arm-unknown-linux-gnueabi- zImage
$ make ARCH=arm CROSS_COMPILE=arm-unknown-linux-gnueabi- modules
$ make ARCH=arm CROSS_COMPILE=arm-unknown-linux-gnueabi- dtbs
```

## Install QEMU
```
sudo apt install qemu-system-arm
```

## Boot QEMU
```
$ QEMU_AUDIO_DRV=none \
qemu-system-arm -m 256M -nographic -M versatilepb -kernel zImage \
-append "console=ttyAMA0,115200" -dtb dts/versatile-pb.dtb
```
setting QEMU_AUDIO_DRV to none is just to suppress error messages from QEMU about missing configurations for the audio drivers, which I do not use.
This will end with a kernel panic and the system will halt. To exit from QEMU, press Ctrl + A and then x.
