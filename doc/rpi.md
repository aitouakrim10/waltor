### Raspberry Pi 3B/3B+ (BCM2837/BCM2837B0)
- Quad-core [cortex A53 ](https://developer.arm.com/Processors/Cortex-A53) (ARMv8) 
- The Raspberry Pi 3B+ has an ARM processor that supports the TrustZone security extension, but it lacks the necessary hardware and firmware support to implement secure boot and a trusted execution environment using TrustZone.
  
### Raspberry Pi 4
  -  Broadcom BCM2711C0 quad-core ARM Cortex-A72 processor (ARMv8)
  - Supports secure boot
  - Supports TrustZone hardware
  - The Cortex-A72 implements the ARMv8-A architecture, which includes TrustZone features:

    - Separate secure and non-secure processor states with hardware access control
    - Secure and non-secure virtual memory mappings
    - Secure interrupts and secure monitor for switching between worlds
    - Secure debug functionality

 
### Raspberry Pi 5 :
    -  Broadcom BCM2712 quad-core Arm Cortex A76 (ARMv8)
    -  Secure Boot Support : hardware supports secure boot capabilities. This allows verifying the bootloader and operating system images using cryptographic signatures before allowing the system to boot.
    -  The secure boot process leverages the on-chip one-time programmable (OTP) memory to store cryptographic keys and hashes used for verification. However, the OTP memory size limits the key size to 2048 bits.
    -  While the Cortex-A76 cores support TrustZone, 
    -  the Raspberry Pi 5's OTP memory has a separate 256-bit region that can be used to store a key for full disk encryption using LUKS
  
### Note:
- SoC vendors licensing ARMv8 cores can choose certain optional features, such as cryptographic acceleration called  ['ARMv8 Cryptography Extensions'](https://developer.arm.com/documentation/ddi0500/e/CJHDEBAF).

- While the Raspberry Pi 3B+ and 4 boards have ARM CPU cores that support TrustZone architecture, the overall SoC hardware lacks critical components for proper isolation between secure and non-secure worlds in TrustZone.
- RPi platform does not have hardware support for secure enclaves

### Radxa Rock 5A / Orange Pi 5 Pro 16GB LPDDR5 Rockchip RK3588S  (Quad Core A76 and Quad Core A55)((octo-core) )
Based on the [RK3588S datasheet](https://www.cnx-software.com/pdf/datasheet/Rockchip-RK3588S-Datasheet%20V1.0-20211221.pdf), the Rock Pi 5B board using this processor would have the following key security features:

    1. TrustZone Support:
    The RK3588S SoC supports the ARM TrustZone technology, which provides hardware-enforced isolation between the secure world and non-secure world. This allows running a secure operating system and trusted applications in the isolated secure world.

    2. Secure Boot:
    The datasheet mentions a "Secure Boot ROM" as part of the security features. This likely refers to support for secure boot functionality, where the bootloader and operating system are cryptographically verified during the boot process to ensure only trusted code is executed.

    3. Cryptographic Accelerators:
    The RK3588S integrates hardware accelerators for various cryptographic operations like encryption, decryption, hashing, and random number generation. This offloads these computationally intensive tasks from the CPU for better performance.

    4. Secure Storages:
    "Secure Key Storage" as one of the security features, indicating the presence of hardware-based secure storage for cryptographic keys and other sensitive data.

### ROCK Pi S :
Based on the [RK3308B datasheet](https://rockchip.fr/RK3308%20datasheet%20V1.1.pdf), the Rock Pi S board using this processor would have the following key security features:

    - TrustZone Technology
    - Cipher Engine:
        Hash Algorithms:
            SHA-1, SHA-256/224, SHA-512/384, MD5 with hardware padding.
        HMAC Support:
            HMAC for SHA-1, SHA-256, SHA-512, MD5 with hardware padding.
        Encryption/Decryption:
            AES-128, AES-192, AES-256 encryption & decryption.
            DES & TDES encryption with ECB, CBC, OFB, CFB modes.
            AES modes: ECB, CBC, OFB, CFB, CTR, CTS, XTS, CCM, GCM, CBC-MAC, CMAC.
        Public Key Algorithms:
            Up to 4096-bit PKA operations for RSA/ECC.
    - Key Management:
        Keyladder Support: Ensures secure key management.
        Secure OTP: Provides a secure, one-time programmable memory for critical security information
    - Random Number Generation
    - Secure Boot 

### NanoPi R4S / Asus Tinker Board
Based on the [Rockchip_RK3399 datasheet](https://opensource.rock-chips.com/images/d/d7/Rockchip_RK3399_Datasheet_V2.1-20200323.pdf)
the NanoPi R4S board using this processor would have the following key security features:

    - support Trustzone technology for the following components inside RK3399
    - support security and non-security mode by software-programmable
    - Embedded dual-channel encryption and decryption engine
        Support AES 128/192/256 bits key mode, ECB/CBC/CTR/XTS chain mode, Slave/FIFO mode
        Support DES/3DES (ECB and CBC chain mode), 3DES (EDE/EEE key mode),Slave/FIFO mode
        Support SHA1/SHA256/MD5(with hardware padding) HASH function, FIFO mode only
        Support 160-bit Pseudo Random Number Generator (PRNG)
        Support 256-bit True Random Number Generator (TRNG)
        Support PKA 512/1024/2048 bit Exp Modulator
    - Support security boot
    - Support security debug


