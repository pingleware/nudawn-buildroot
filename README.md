# NuDawn (by buildroot)
Starting with a clean build,

	git clone git://git.buildroot.net/buildroot

or

	make --directory buildroot clean

then following a new build

	make --directory buildroot

upon completiong, there will exists only,

	output/images/rootfs.tar

To test this with qemu,

	qemu-system-x86_64 -M pc -kernel output/images/rootfs.tar

and nothing happens, because we need a kernel,

## Configuring the Kernel
Start,

	make --directory buildroot menuconfig

	In Kernels --> Linux Kernel
               defconfig = i386

	In Toolchain --> Enable C++ Support
	In Bootloaders --> syslinux
	In Filesystem images --> isoimage
	In Target packages --> Text editors and views --> nano
	In Target packages --> Network application --> dnsmasq

then save and exit,

now configure the linux kernel by

	make --directory buildroot linux-menuconfig

then rebuild,

	make --directory buildroot

To test qemu with networking support,

	qemu-system-i386 -serial stdio -cdrom buildroot/output/images/rootfs.iso9660 -m 256 -M pc -nic user,model=virtio-net-pci

or create a test.sh

	echo qemu-system-i386 -serial stdio -cdrom buildroot/output/images/rootfs.iso9660 -m 256 -M pc -nic user,model=virtio-net-pci > test.sh && sudo chmod +x test.sh

