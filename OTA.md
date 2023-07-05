## Over-The-Air (OTA) Update using pre-built Images

### ATTENTION for pre-flashed boards
If you bought an OpenDTUFusion Board that had a pre-flashed firmware, you might lose radio module connection after using the generic OTA image when you OTA for the first time,
as the baked-in pin assignments get overridden.
If that is the case for you, please load the openDTUFusion-specific device_profile JSON to restore them, they will then also be retained over future OTA updates.
The How-To for that is here: https://github.com/markusdd/OpenDTUFusionDocs/blob/main/FLASHED_START.md#loading-a-device-profile-for-the-rf-and-display-pinout

## OTA Tutorial
OpenDTU now offers generic ESP32-s3 builds [here](<https://github.com/tbnobody/OpenDTU/releases>). For the Fusion board, you need the USB version (as we use the in-built USB and no external converter):

![ReleaseIMages](pics/ReleaseImages.png)

For Over-the-Air (OTA) updates, download the non-factory .bin marked in green.

Then go to the web interface, select and flash it.

![OTA](pics/OTA.png)

![OTAImageSelect](pics/OTAImageSelect.png)

Wait for it...

![OTAProgress](pics/OTAProgress.png)

Done.

![OTADone](pics/OTADone.png)
