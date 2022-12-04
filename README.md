# NuDawn (by buildroot)
Starting with a clean build,

	git clone git://git.buildroot.net/buildroot

or

	cd buildroot && make clean

then following a new build

	make

upon completiong, there will exists only,

	output/images/rootfs.tar

To test this with qemu,

	qemu-system-x86_64 -M pc -kernel output/images/rootfs.tar

and nothing happens, because we need a kernel,

## Configuring the Kernel
Start,

	make menuconfig

	In Kernels --> Linux Kernel
               defconfig = i386

	In Toolchain --> Enable C++ Support
	In Bootloaders --> syslinux
	In Filesystem images --> isoimage
	In Text editors and views --> nano
	In Network application --> dnsmasq

then save and exit,

now configure the linux kernel by

	make linux-menuconfig

then rebuild,

	make

To test qemu with networking support,

	qemu-system-i386 -serial stdio -cdrom output/images/rootfs.iso9660 -m 256 -M pc -nic user,model=virtio-net-pci

or create a test.sh

	echo qemu-system-i386 -serial stdio -cdrom output/images/rootfs.iso9660 -m 256 -M pc -nic user,model=virtio-net-pci > test.sh && sudo chmod +x test.sh

# Enable overlay

	BR2_ROOTFS_OVERLAY
