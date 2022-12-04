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

![BUILDROOT Main Index](images/buildroot-001.png)

	In Kernels --> Linux Kernel

![BUILDROOT](images/buildroot-002.png)

               defconfig = i386

![BUILDROOT](images/buildroot-003.png)
![BUILDROOT](images/buildroot-004.png)
![BUILDROOT](images/buildroot-005.png)

	In Toolchain --> Enable C++ Support

![BUILDROOT](images/buildroot-006.png)

	In Bootloaders --> syslinux

![BUILDROOT](images/buildroot-007.png)

	In Filesystem images --> isoimage

![BUILDROOT](images/buildroot-008.png)

	In Target packages --> Text editors and views --> nano

![BUILDROOT](images/buildroot-009.png)

	In Target packages --> Network application --> dnsmasq

![BUILDROOT](images/buildroot-010.png)

then save and exit,

![BUILDROOT](images/buildroot-011.png)

now configure the linux kernel by

	make --directory buildroot linux-menuconfig

then rebuild,

	make --directory buildroot

To test qemu with networking support,

	qemu-system-i386 -serial stdio -cdrom buildroot/output/images/rootfs.iso9660 -m 256 -M pc -nic user,model=virtio-net-pci

or create a test.sh

	echo qemu-system-i386 -serial stdio -cdrom buildroot/output/images/rootfs.iso9660 -m 256 -M pc -nic user,model=virtio-net-pci > test.sh && sudo chmod +x test.sh


# Additional Helpful Links
The following links can provide additional resoruces and assistance,

	https://buildroot.org/downloads/manual/manual.html)
	https://www.thirtythreeforty.net/posts/2020/01/mastering-embedded-linux-part-3-buildroot/
	https://ja.nsommer.dk/articles/linux-and-tiny-c-compiler-in-the-browser-part-one.html
	https://hackaday.com/2022/05/28/linux-and-c-in-the-browser/ 

