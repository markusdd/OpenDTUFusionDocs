# OpenDTU Fusion Documentation

**HINT:** For the new **CAN/Iso** extension shield for use with e.g. OpenDTU-OnBattery click [here](CANIso.md).

**HINT:** For the **PoE** extension shield click [here](POE.md).

![overview](pics/overview.png)

## Where to get?

You can buy the OpenDTU Fusion board (and fitting 3D-printed cases when you don't want to [build your own](#suitable-housings-for-diy-3d-printing)) at the AllianceApps Community Shop here:
<https://shop.allianceapps.io/products/opendtu-fusion-community-edition>

Simple 800MHz-2.6GHz wideband PCB Antennas are included and sufficient for most users. Later also a variant with external SMA-Antennas will be available if you have deep coverage requirements.
Meanwhile you can have this by ordering the U.FL-SMA-pigtails and Antennas yourself, you need 1x 2.4GHz for Wifi, 1x 2.4GHz for the NRF24 (for HM Series) and one 868MHz Antenna for the CMT2300A-RF (HMS/HMT series). If you only operate one type of inverter series, you can leave the not needed antenna port unpopulated.

**HINT about Flash Size**: As people have requested this info because e.g. OpenDTU-OnBattery considers moving away from supporting 4MB Flash: The ESP32-S3 module on the Fusion will always come with at least 8MB Flash and 2MB PSRAM (8NR2).
We might elect to supply more if parts availability demands it but we gurantee not to deliver anything below this configuration.

About board revisions see [the revisions page](REVISIONS.md).

## Summary

OpenDTU Fusion is a very dense and small board which combines an
Espressif ESP32-S3-WROOM-1U module together with a
Nordic NRF24LP01+, Skyworks RX2401C low noise amplifier in the 2.4GHz band and a CMT2300A 868MHz RF to provide a stable hardware base for [OpenDTU](https://github.com/tbnobody/OpenDTU) and [AhoyDTU](https://github.com/lumapu/ahoy) opensource firmwares
to monitor and control Hoymiles HM, HMS and HMT solar inverters (as well as their
technically similar cousins like some Solenso or TSUN models).

Why another Open/AhoyDTU PCB you might ask?

The common solutions to buy seperate modules, soldering pin headers and using adapter PCBs are totally fine, but many people have issues with them. They might not be into electronics, but don't want to buy an expensive Hoymiles DTU, which costs a lot of money and forces you to use their cloud service. Some of the cheap NRF24 modules use fake chips that have issues, they cheap out on the RF design, and the PCB antennas meet their limits when there is more than 1 or 2 walls in the way. Some leave out the amplifier, further incerasing issues with reception performance.
With version 2, which integrates the NRF and CMT RF modules, you even get something not even Hoymiles has themselves: You have one super compact device that can work with all inverter series they offer, no matter if they use the 2.4GHz or 868MHz type communication.

So, with OpenDTU Fusion you get:

- no soldering of pin headers, or any parts of any kind
- a very compact form factor of just 5.5cm x 5.5cm to fit in your favorite case
- proper RF path layout and parts according to the manufacturer datasheets with proper thermal design, impedance matching etc.
- full antenna flexibility though U.FL/IPEX connectors: from a small PCB antenna adhered to your case to the full +8dBi external powerhouse everything is possible to fit your application
- full feature set of the ESP32-S3, flash/debug/monitor just by using a single USB-C cable

For detailed specs see the corresponding section below.

Many thanks to the OpenDTU/AhoyDTU community for providing reviews, testing and other valuable input. And KiCad for making such awesome open source PCB software.

## How-To Setup

First, make sure your system is setup to deal with ESP devices. For that look at the [drivers](DRIVERS.md) section.
If you face issues with the drivers or flashing, refer to the [troubleshooting](TROUBLESHOOTING.md) guide.

Depending on if you bought a OpenDTU Fusion board that has OpenDTU already flashed, or you have a fresh new blank (or erased) board, or just want to update:

1) First, setup the board hardware like described [here](HW_SETUP.md)
2) For blank/erased boards go [here](BLANK_START.md)
3) For already flashed boards go [here](FLASHED_START.md)
4) For OTA update via the Web GUI go [here](OTA.md)

## Specs

- Size: 5.5cm x 5.5cm, 4x M3 corner mounting holes (46.5-47mm pitch) (if you wish to design a case for this PCB yourself a 3D model step file is available [here](3d/OpenDTUFusion2.step), note that the PCB process has about 0.2mm tolerance on both hole pitch and board outline and the holes are plated, which reduces diameter by about 0.2mm compared to the step file)
- Power: 5V via USB-C or 5V DC via screw terminal, selectable by a 2.54mm jumper
- Wireless: UF.L/IPEX Antenna connectors to enable you to either use self-adhering PCB-Antennas or SMA-antennas outside your case for best send/receive performance
(IMPORTANT: these are full-size U.FL/IPEX connectors, not the 'mini' versions found on some newer laptop Wifi cards, which are often called U.FL/IPEX/MHF 4 or Gen4)
- USB-C connector with proper ESD-protection that provides all-in-one flashing/debugging/console monitor and power supply, no more extra USB/UART bridges or debug cables/probes required
- power supply secured by a self-resetting fuse should stuff go wrong -> no more soldering of SMD-Fuses to replace them
- a high-quality (Renesas ISL3178E or Texas Instruments THVD1429DR) half-duplex RS485 Transceiver for e.g. Modbus applications
- 2 programmable LEDs connected directly to two of the ESP32-S3 GPIOs and a power indicator LED
- reverse polarity protection on the 5V DC screw terminal
- all the pin headers you will need:
  - I2C for sensors or displays
  - SPI header for e.g. eInk displays including 2 GPIO control lines
  - UART and JTAG header for classic access to flashing, monitoring console and debug (can also be used for other general purposes in software)
  - RS485 header to connect the A and B lines

## Suitable housings for DIY 3D printing

- Simple DTU Fusion Case without display by semy3d.de
  https://semy3d.de/mediafiles/STL/Fusion%20Case.rar

- OpenDTU Fusion + POE HAT Case without Display by hmarius1:
  Housing for Fusion board including support for the optional [PoE Shield](POE.md) and 3 external antennas
  https://www.thingiverse.com/thing:6371201
 
## IMPORTANT Application Notes

In general, follow the guidelines provided by the awesome [OpenDTU](https://github.com/tbnobody/OpenDTU) and [AhoyDTU](https://github.com/lumapu/ahoy) projects.

This documentation will mainly focus on the differences that this integrated board brings,
especially the more modern ESP32-S3 chip and its integrated USB-interface and the specific pin-out.

For how to generally build/deploy the DTU firmwares and using them, refer to the original projects above.

The R16 resistor is a not populated 0805 SMD footprint connected to the A and B RS485 lines.
It can be used to place an optional 120 Ohm termination resistor if that is desired for the application.

If you wish to write software yourself for this board or do some more advanced things a
detailed pin-out is available at the bottom of this document.
For all others, it is recommended to use the pre-configured build targets and device profile files in ahoy and openDTU for this board, which contain the correct pinout already.

## Pin mapping of the ESP32-S3 on OpenDTU Fusion v2.x

The ESP32-S3 can map any GPIO function pretty much anywhere through firmware, but this is strictly for advanced users and developers who know what they are doing. So be warned, you are on your own from here.

Please note that the display SPI pin names are derived from typical eInk displays that are available, the naming and function might differ for other models. Check the function mapping
with the proper OpenDTU/AhoyDTU version that has support for those special displays.
In general, these pins can be used for any arbitrary funtion, just like the ones on the I2C, UART and JTAG headers.

The ESP32-S3 has many amazing internal peripherals that can be brought out, either with simple GPIO-functions or for sensors, touch, etc.
See the databook for all details.

**HINT:** When using the [PoE Shield](POE.md), the relevant pins for the W5500 connection are marked in braces with "(Ethernet: ...)"

**HINT:** When using the [CAN/Iso Shield](CANIso.md), the relevant pins for the CAN/Isolator connections are marked in braces with "(CAN/Iso: ...)".
To avoid confusion with TX/RX denomination also please look at the example device profile in the [CAN/Iso Shield](CANIso.md) documentation.

|GPIO|Freely mappable|Connected To|Comment|
|----|--------------|------------|-------|
|GPIO0 |no|Boot button|ESP32-S3 special strapping pin|
|GPIO1 |yes|SCL|on I2C header|
|GPIO2 |yes|SDA|on I2C header|
|GPIO3 |no|GPIO2 CMT|hardwired to CMT2300A RF (strapping pin, do not burn JTAG sel efuse!)|
|GPIO4 |no|CSB CMT|hardwired to CMT2300A RF|
|GPIO5 |no|SDIO CMT|hardwired to CMT2300A RF|
|GPIO6 |no|SCLK CMT|hardwired to CMT2300A RF|
|GPIO7 |no|GPIO1 CMT|hardwired to CMT2300A RF|
|GPIO8 |no|GPIO3 CMT|hardwired to CMT2300A RF|
|GPIO9 |yes|MOSI display|on SPI display header (CAN/Iso: Iso1 Ext RX / ESP TX)|
|GPIO10|yes|SCK display|on SPI display header (CAN/Iso: Iso1 Ext TX / ESP RX)|
|GPIO11|yes|CSN display|on SPI display header (CAN/Iso: Iso2 Ext TX / ESP RX)|
|GPIO12|yes|DC display|on SPI display header (CAN/Iso: Iso2 Ext RX / ESP TX)|
|GPIO13|yes|RST display|on SPI display header (CAN/Iso: CAN RX)|
|GPIO14|yes|MISO (busy) display|on SPI display header (CAN/Iso: CAN TX)|
|GPIO15|no|RE_N RS485|hardwired to RS485 transceiver|
|GPIO16|no|R RS485|hardwired to RS485 transceiver|
|GPIO17|no|D2 (MQTT) blue LED|connected by R12 560 Ohm resistor|
|GPIO18|no|D3 (INV ON) white LED|connected by R13 3.3k Ohm resistor|
|GPIO19|no|USB_D-|USB differential data line|
|GPIO20|no|USB_D+|USB differential data line|
|GPIO21|no|FSCB CMT|hardwired to CMT2300A RF|
|GPIO22|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO23|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO24|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO25|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO26|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO27|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO28|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO29|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO30|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO31|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO32|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO33|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO34|no|n/a (not exposed)|used inside ESP32-S3-WROOM-1U module|
|GPIO35|no|MOSI NRF24|hardwired to Nordic RF|
|GPIO36|no|SCK NRF24|hardwired to Nordic RF|
|GPIO37|no|CSN NRF24|hardwired to Nordic RF|
|GPIO38|no|CE NRF24|hardwired to Nordic RF and Skyworks LNA|
|GPIO39|yes|TCK|ESP32-S3 default JTAG pins (Ethernet: W5500 SCLK)|
|GPIO40|yes|TDO|ESP32-S3 default JTAG pins (Ethernet: W5500 MOSI)|
|GPIO41|yes|TDI|ESP32-S3 default JTAG pins (Ethernet: W5500 MISO)|
|GPIO42|yes|TMS|ESP32-S3 default JTAG pins (Ethernet: W5500 CS)|
|GPIO43|yes|UART_TX|ESP32-S3 default serial console (Ethernet: W5500 RST)|
|GPIO44|yes|UART_RX|ESP32-S3 default serial console (Ethernet: W5500 INT)|
|GPIO45|no|D RS485|hardwired to RS485 transceiver (strapping pin, pull-down 100k Ohm)|
|GPIO46|no|DE RS485|hardwired to RS485 transceiver (strapping pin, pull-up 10k Ohm)|
|GPIO47|no|IRQ NRF24|hardwired to Nordic RF|
|GPIO48|no|MISO NRF24|hardwired to Nordic RF|
