
### How to Use Raspberry Pi5 Secure Boot
For more information about enabling secure-boot please see 

-   [the Secure Boot readme](https://github.com/raspberrypi/usbboot/blob/master/Readme.md#secure-boot) 
-   [Pi5 secure-boot bootloader flash and OTP provisioning](https://github.com/raspberrypi/usbboot/blob/master/secure-boot-recovery5/README.md)
-   [Secure Boot tutorial](https://github.com/raspberrypi/usbboot/blob/master/secure-boot-example/README.md)
-   [Program a key into OTP with rpi-otp-private-key](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#program-a-key-into-otp-with-rpi-otp-private-key)


### Prerequisites
1. **Separate Device**: Use another Raspberry Pi, a laptop, or similar running Linux.
2. **Install Essential Packages**:
    ```sh
    sudo apt install xxd python3-pycryptodome
    sudo apt install git libusb-1.0-0-dev pkg-config build-essential
    git clone --recurse-submodules --shallow-submodules --depth=1 https://github.com/raspberrypi/usbboot
    cd usbboot
    make
    sudo ./rpiboot
    ```
3. **Updating the rpi-eeprom submodule** 
   
    After updating the usbboot repo  update the submodules by running
    ```sh
        git pull --rebase origin master
        git submodule update --init
    ```

### Creating an RSA Key Pair

1. **Generate a 2048-bit RSA Private Key**:
    ```sh
    openssl genrsa 2048 > private.pem
    ```
2. **Generate a Public Key from the Private Key**:
    ```sh
    openssl rsa -in private.pem -out public.pem -pubout -outform PEM
    export KEY_FILE="${HOME}/private.pem"
    ```
   **Warning**: Keep these keys secure to prevent unauthorized access.

### Update the EEPROM

1. **EEPROM config**:

   Setting `SIGNED_BOOT=1` enables signed-boot mode so that the bootloader will only boot.img files signed with the specified RSA key. Since this is an EEPROM config option secure-boot can be tested and reverted via RPIBOOT at this stage.
    
    See: [Bootloader configuration](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#raspberry-pi-bootloader-configuration)

2. **Sign the EEPROM and the second stage bootloader**
   
   The BCM2712 boot ROM requires the second stage firmware (`recovery.bin` / `bootcode5.bin`) to be counter-signed with the customer private key in secure-mode. Pass the f flag to enable firmware counter-signing.
   ```sh
    ../tools/update-pieeprom.sh -f -k "${KEY_FILE}"
   ```
    If secure-boot has already been enabled on the device then `recovery.bin` must then also be counter-signed.
    However, booting a counter-signed `recovery.bin` image on a fresh board without secure-boot enabled will fail because the ROM is effectively checking this against a key hash of zero.
    ```sh
    ../tools/update-pieeprom.sh -fr -k "${KEY_FILE}"
   ```
    ```bash
     Flags:
    -f Countersign the EEPROM firmware
    -r Countersign recovery.bin. Once secure-boot has been enabled (but not
       before!) the recovery.bin file must be countersign in addition to
       bootcode.bin.

    The -k argument signs the EEPROM configuration using the specified RSA 2048 bit private key in PEM format. It also embeds the public portion of the RSA key pair in the EEPROM image so that the bootloader can verify the signed OS image.
   ```

    `pieeprom.bin` can then be flashed to the bootloader EEPROM via `rpiboot`.

     Program the EEPROM image using rpiboot
    * Power off DUT
    * Set nRPIBOOT jumper (or hold power button before power on) and remove EEPROM WP protection
        ```bash
        cd secure-boot-recovery5
        ../rpiboot -d .
        ```
    * Power ON the DUT
### Note :
open the `main.c` file , modify the value of `char * directory ` variable to  mass-storage-gadget64 path
```sh
    char * directory = path/to/mass-storage-gadget64/path
```


### Locking secure-boot mode

After verifying that the signed OS image boots successfully the system can be locked into secure-boot mode. This writes the hash of the customer public key to "one time programmable" (OTP) bits. From then onwards:

        -   The 2712 boot ROM verifies that the secondstage firmware (recovery.bin / bootsys) are signed with the customer private key in addition to the Raspberry Pi private key.
        -   The bootloader will only load OS images signed with the customer private key.
        -   The EEPROM configuration file must be signed with the customer private key.
        -   It is not possible to downgrade to an old version of the bootloader that doesn't support secure boot.
        -   BETA bootloader releases are not signed with the ROM secure boot key and will not boot on a system where revoke_devkey has been set.
    
To enable this edit the `config.txt` file in this directory and set `program_pubkey=1`

`program_pubkey` - If 1, write the hash of the customer's public key to OTP.

#### Creating a Signed Boot Image 

1. **Refer to the GitHub usbboot Repository**:
    - Complete instructions are found at [usbboot#secure-boot](https://github.com/raspberrypi/usbboot#secure-boot).
    - Example usage at [secure-boot-example](https://github.com/raspberrypi/usbboot/blob/master/secure-boot-example/README.md).


#### Using the Mass Storage Gadget on a Secure Boot System

1. **Sign the usbboot Image**:
    ```sh
    cd secure-boot-msd
    ../tools/rpi-eeprom-digest -i boot.img -o boot.sig -k "${KEY_FILE}"
    ```
2. **Run rpiboot**:
    ```sh
    ../rpiboot -d .
    ```
   **Warning**: Keep the signed usbboot image secure to prevent unauthorized data recovery.

By following these steps, you will establish a secure boot process for your Raspberry Pi 5, ensuring that only trusted, signed software can be executed. For any additional details or updates, refer to the Raspberry Pi Ltd GitHub repository.









