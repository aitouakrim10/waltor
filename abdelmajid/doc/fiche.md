
## boot.img
---- 

### Kernel
To build the kernel, I used the default configuration and enabled only the kexec features using [linux](https://github.com/raspberrypi/linux).

This GitHub repository allows us to build:
- `kernel_2718.img`
- `bcm----.dtb`
- `overlays/*.dtb`
- Kernel modules (***)

[For more information](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#cross-compiled-customisation).

### rootfs.cpio.zst
To build the root filesystem, I used the [Buildroot signed-boot branch](https://github.com/raspberrypi/buildroot/tree/raspberrypi-signed-boot). From this program, I obtained `rootfs.cpio.zst`.

I decompressed this archive, installed the kernel modules (***) and recompressed the files to get a new `rootfs.cpio.zst`.

### config.txt/cmdline.txt
I wrote these files.

### Image
I combined all files into `boot.img`.

### Results
- Successful boot process.
- When we create a file or repository in this mode (secure boot), the creation is temporary. If we reboot, the file system returns to its initial state, discarding all modifications.

