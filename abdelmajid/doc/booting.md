
## HTTP/HTTPS boot
----
### Documents
   -  [raspberry pi (github)](https://github.com/raspberrypi/documentation/blob/develop/documentation/asciidoc/computers/raspberry-pi/boot-http.adoc)
   -   [raspberry pi (documentation)](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#http-boot)

#### Requirements 
   -   update to a bootloader released 10th March 2022 or later.
   -   requires a wired Ethernet connection
   -   To use custom CA certificates, update to a bootloader released 5th April 2024 or later. Only devices running the BCM2712 CPU support custom CA certificates.  

### Configuartion 
Add the following lines to [EEPROM](https://github.com/raspberrypi/rpi-eeprom/)
```bash
      [gpio8=0]
      BOOT_ORDER=0xf7 # Try SD card first, then USB mass storage, then network boot.
      HTTP_HOST=<your_website>
      HTTP_PATH=<path_to_files>
      NET_INSTALL_ENABLED=0 # Disables the interactive network install feature,
```

### keys :
```bash
$ rpi-eeprom-config -c boot.conf -p mypubkey.pem -o pieeprom.upd pieeprom.original.bin #add your public key to the EEPROM
$ rpi-eeprom-digest -i pieeprom.upd -o pieeprom.sig #generate a signature for EEPROM
$ rpi-eeprom-digest -i boot.img -o boot.sig -k myprivkey.pem # sign the network install image with private key then  put boot.img and boot.sig on the server
```

### Enable secure HTTP (HTTPS)
```bash
$ openssl x509 -in your_ca_root_cert.pem -out cert.der -outform DER # generate a DER-encoded certificate
$ sha256sum cert.der  #  generate a SHA-256 hash of the certificate
$ sudo rpi-eeprom-config --edit
## add this line HTTP_CACERT_HASH=<hash>
#### load everything into EEPROM
$ rpi-eeprom-config -c boot.conf -p mypubkey.pem -o pieeprom.bin --cacertder cert.der pieeprom.original.bin
$ rpi-eeprom-digest -k myprivkey.pem -i pieeprom.bin -o pieeprom.sig
```
## Enable Secure boot

   -  [secure-boot-recovery](https://github.com/raspberrypi/usbboot/blob/master/secure-boot-recovery/README.md)
   -  [Enabling UEFI Secure Boot](https://github.com/tianocore/tianocore.github.io/wiki/How-to-Enable-Security)
  

---
#### NOTE : HTTP boot require a ethernet connection 
   *  Use Devices provide Ethernet ports and can be used for network booting.
---

### uboot
   -  U-Boot [supports HTTP / TFTP](https://www.linaro.org/blog/ledge-blogs-uefi-http-and-https-boot-in-u-boot/)
   -  The support for [HTTPS is under development](https://www.linaro.org/blog/http-now-supported-in-u-boot/), but it is not yet fully integrated or available in the main version of U-Boot.
  
Include in `boot.img` the minimum files needed to create a tunnel


### Summury 
The Raspberry Pi supports HTTPS booting, requiring a bootloader update (bootloader released 10th March 2022 or later) and a wired Ethernet connection. 
Since U-Boot does not yet support secure network protocols( supports tftp and http but not https ), all necessary files for the minimal system to setup a VPN should be included in `boot.img`.
