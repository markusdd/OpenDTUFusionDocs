# OpenDTU Fusion Board Revisions

## v1
Version 1 was only ever available as a prototype within the development and tester community. It only contains the NRF24 and no CMT2300A for 868MHz yet. It's recognizable by it's
green PCB color and flat SPI display connector. It is incompatible with the PoE and CAN/ISO shields.

## v2.0 
Prototyping run for the black version 2 OpenDTU Fusion as it is known today. It is compatible with all shields and comes with both the CMT2300A RF for 868MHz communications as well as the NRF24.

## v2.1 
The first production version from mid of 2023 to June 2024. It contains some layout optimzation compared to v2.1 like improved ground stitching, crystal island isolation etc. .
Also the BOM has been optimized for cost, EMC and performance. It is fully compatible with all shields. The minimum ESP32-S3 configuration is 8NR2, meaning 8MB of Flash and 2MB of external PSRAM.
There are no limitations for PSRAM use.

## v2.2 
Production version starting in July 2024. It contains some BOM updates invisible to software to adjust for parts that have become obsolete (e.g. the blue LED is now a new part number). The ESP32-S3 is now coming in N16R8 (16MB Flash, 8MB PSRAM) configuration to accomodate more memory intensive OpenDTU Forks like OpenDTU on Battery which are looking into deprecating smaller Flash size configs.
This version remains compatible with all released shields.

**IMPORTANT** For v2.2 you can either use the PSRAM or the NRF24. Due to an internal limitation of the Espressif WROOM-1U module, the PSRAM blocks some of the SPI Pins for internal use of the larger PSRAM. This does not matter for normal OpenDTU as it does not make use of PSRAM in the standard builds. If you do custom builds with PSRAM make sure NRF24 is disabled in your config and none of the pins are assigned to it otherwise the device will not boot!