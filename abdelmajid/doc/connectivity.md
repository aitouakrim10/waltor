#### Raspberry pi  networking [specs](https://www.raspberrypi.com/documentation/computers/getting-started.html#networking) :
* it comes with Wi-Fi and Bluetooth connectivity.
* The `Model B` suffix indicates variants with an Ethernet port; `Model A` indicates no Ethernet port. If your Raspberry Pi doesn’t have an Ethernet port, you can still connect to a wired internet connection using a USB-to-Ethernet adapter.

#### BOOT ROM / Uboot :  HTTP-BOOT 
* wired Ethernet connection required
    *  use bridge or adapter [application (network boot)](https://raspberrytips.com/network-boot-with-raspberry-pi/)

#### Uboot: [UEFI HTTP Boot](https://docs.u-boot.org/en/latest/develop/uefi/uefi.html#uefi-http-boot)
 * supports Ethernet for network booting
 * No Native Wireless Support
### 5G connectivity

#### Hardware:

    * 5G Router/Modem: Purchase a 5G router or modem compatible with the chosen service provider.
    Antennas: Consider using external 5G antennas to improve signal reception.
    * Power Supply: Ensure a reliable power supply for the 5G hardware, possibly through solar panels or generators if the area lacks electricity.
#### Note :
for http-boot ,Use a 5G router that includes Ethernet ports

#### Configuration :
  
  * [Router setup](https://www.wikihow.com/Configure-a-Router)
  * [Firewall/Security](h)
  
example : [Cisco Router Configuration](https://www.networkstraining.com/basic-cisco-router-configuration-steps/) , [Configuring firewall rules](https://help.keenetic.com/hc/en-us/articles/360001434079-Configuring-firewall-rules-from-the-command-line-interface)

### PCIe to 5G/4G/3G HAT designed for Raspberry Pi 5 :
  * The HATs often require driver installation and configuration, which typically required an operating system
  
example : [RM520N-GL 5G HAT+](https://www.waveshare.com/wiki/RM520N-GL_5G_HAT+)