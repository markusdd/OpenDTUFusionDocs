# OpenDTU Fusion PoE Shield Documentation

The OpenDTU Fusion Shield is an extension Board specifically made to fit on top of the OpenDTU Fusion base board from v2.0 and later.
It provides a possibility to power the Fusion board via Power over Ethernet and optionally also use an Ethernet data connection via the also included W5500 100MBit/s Ethernet chip, that connects to the ESP32-S3 on the base board via SPI. Additonally, the modbus header from the base board now leads to a screw terminal for easier install.

Both the display headers for I2C and SPI (for eInk) are connected through, so display configurations can still be used.

**IMPORTANT: This board strictly follows IEEE 802.3af Class 0 for PoE power delivery. Power injector adapters which just provide 48V or 24V passively without any negotiation will not work! (e.g. Unifi access points came with those passive 24V power ethernet injectors early on, these will not work and are not standard compliant!)**

The community has tested the board with several PoE capable switches out there from TP-Link, Netgear, Unifi and Aruba and all have worked. Just make sure your switch or PoE injector supports IEEE 802.3af and you should be good.

When raising issues, ALWAYS provide info against which hardware you have tested and make sure, if it all possible, you tried an alternative switch or adapter before you raise an issue. If you own a multimeter, providing a measurement of the output voltage also is helpful.