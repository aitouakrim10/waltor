# WalT on the Roof


## investigation : security feature in the RPi / clones
[Raspberry Pi (RPI)](./doc/rpi.md) features ARM CPU cores with TrustZone support, lacking critical components for full isolation. RPI 4 and 3b+ offer hardware-backed secure boot using on-chip OTP memory, but may miss integral TrustZone components. Additionally, RPI lacks hardware support for secure enclaves , Integrating a Hardware Security Module (HSM) (for example : [ATECC608](./doc/crypto.md) ) into RPI can enhance its security by adding capabilities like Key Management (secure storage for cryptographic keys)
and Physical tamper detection that involves tamper-evident enclosures and circuitry that detect physical access attempts. If tampering is detected, the HSM automatically zeroizes or erases all sensitive cryptographic keys and data to prevent their compromise.s

[Advantages of RPI Clones](./doc/rpi.md):
RPI clones like Radxa Rock 5A, ROCK Pi S, and NanoPi R4S offer TrustZone support, secure boot, cryptographic accelerators, key management, and random number generation.
These clones provide hardware-enforced isolation between secure and non-secure worlds, ensuring a higher level of security compared to standard RPI Socs.

## HTTPS Booting
The Raspberry Pi supports [HTTPS booting](./doc/boot.md), requiring a bootloader update (bootloader released 10th March 2022 or later) and a wired Ethernet connection.
[U-Boot](./doc/boot.md#u-boot) does not yet support secure network protocols( supports tftp and http but not https ),
### secure boot and OTP provising
*   [documents](./doc/secure_boot/)
### Connectivity 
Raspberry Pi networking [specs](./doc/connectivity.md) includes Wi-Fi and Bluetooth on most models, with Model B variants featuring Ethernet ports and Model A lacking them (USB-to-Ethernet adapters can be used). HTTP-Boot requires a wired Ethernet connection, and lacks native wireless support. For 5G connectivity, additional hardware like a compatible router/modem and reliable power supply are needed, with router setup and security configuration required. 
PCIe to 5G/4G/3G HATs for Raspberry Pi 5 require driver installation and configuration, which typically necessitates an operating system.
