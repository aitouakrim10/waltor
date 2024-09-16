
## HTTP/HTTPS boot
----
### Documents
   -  [raspberry pi http-boot (github)](https://github.com/raspberrypi/documentation/blob/develop/documentation/asciidoc/computers/raspberry-pi/boot-http.adoc)
   -   [raspberry pi http-boot (documentation)](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#http-boot)

### [Requirements ](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#requirements)
   -   requires a wired Ethernet connection
   -   update to a bootloader released 10th March 2022 or later.
   -   To use custom CA certificates, update to a bootloader released 5th April 2024 or later. Only devices running the BCM2712 CPU support custom CA certificates.  
  
## U-boot :
---
   * [RPi U-Boot](https://elinux.org/RPi_U-Boot)
   *  [Configuring UEFI secure boot](https://docs.u-boot.org/en/v2021.04/uefi/uefi.html#configuring-uefi-secure-boot)
   *  `U-boot` supports HTTP but does not yet support HTTPS (for more details, see [this blog post](https://www.linaro.org/blog/ledge-blogs-uefi-http-and-https-boot-in-u-boot/)), for more informations you can refer to the : [U-boot Documentation](https://docs.u-boot.org/en/latest/develop/uefi/uefi.html#uefi-http-boot) 
   *  prapre SD card : [Deploy u-boot](https://gist.github.com/Semant1ka/fe2feac86ac57db5dcea97fb21a2c96c) (if we want to get U-Boot from SD card)
  


### Summury 
The Raspberry Pi supports HTTPS boot, requiring a bootloader update (bootloader released 10th March 2022 or later) and a wired Ethernet connection. 

