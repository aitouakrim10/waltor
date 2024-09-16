## KEXEC and Raspberry Pi 5 Setup
----

### [Build the Kernel](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#content)

Start by cloning the Raspberry Pi Linux repository:

```sh
git clone --depth=1 https://github.com/raspberrypi/linux
```

#### [Cross-compile the Kernel](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#cross-compile-the-kernel)

Install the necessary tools for cross-compilation:

```sh
sudo apt install bc bison flex libssl-dev make libc6-dev libncurses5-dev
sudo apt install crossbuild-essential-arm64  # This installs the 64-bit toolchain to build a 64-bit kernel
```

Navigate to the Linux directory and set up the kernel configuration:

```sh
cd linux
KERNEL=kernel_2712
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- bcm2712_defconfig
```

#### Configure the Kernel

To further customize your kernel, install additional dependencies and open the configuration menu:

```sh
sudo apt install libncurses5-dev
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- menuconfig
```

In the menu, navigate and configure the following options:

- **General setup** > **Kexec and crash features**: Enable all features by marking them with `(*)`.
- Ensure that **Profiling support** is enabled (`(*)`).
- **File systems** > **Pseudo filesystems**: Enable all relevant proc files (e.g., `kcore`, `vmcore`, etc.) by marking them with `(*)`.

After making your selections, save the configuration.

To build the 64-bit kernel, run:

```sh
make ARCH=arm64 CROSS_COMPILE=aarch64-linux-gnu- Image modules dtbs
```

Once the build is complete, follow the instructions in [Install the kernel](https://www.raspberrypi.com/documentation/computers/linux_kernel.html#cross-compiled-install) to install it on your Raspberry Pi.

### Final Steps

1. **Update `config.txt`**:  
   Add the following line to your `config.txt` file to specify your new kernel:

   ```sh
   kernel=your-new-kernel.img  # If you used the name from the guide, this would be kernel_2712.img
   ```

2. **Update `cmdline.txt`**:  
   Add `nr_cpus=1` to `cmdline.txt` to limit the system to a single CPU core. [Learn more about this option](https://www.thegoodpenguin.co.uk/blog/booting-linux-from-linux-with-kexec/).

Finally, reboot your Raspberry Pi and use `kexec` with the `-s` option to load the new kernel.