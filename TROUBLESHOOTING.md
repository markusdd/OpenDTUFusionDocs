## Troubleshooting

When trying to flash you might see something like this:

![UploadError](pics/UploadError.png)

This might indicate that:

- a driver is missing
- permissions are off
- driver is installed but not selected for the device

### Windows

Check, when board is connected and in bootloader-mode, that what you see in Device Manager is similar to this. There should be one generic COM port (number might differ) and a JTAG/Debug device.

![DeviceManager](pics/DeviceManager.png)

For the debug device, make sure not the generic windows driver is used, but the one from Espressif:

![VerifyEspressifDriver](pics/VerifyEspressifDriver.png)

If this is not the case, choose 'Update Driver' and then 'automatically'. When you installed the Espressif drivers as instructed, it should switch to it. If it doesn't, do the manual selection.

![AutomaticallySelectDriver](pics/AutomaticallySelectDriver.png)

For the COM port, it should just be the generic Windows serial device driver.

### Linux

Executing `lsusb` should return something like this when the boards is connected:

![lsusbEspressifDebug](pics/lsusbEspressifDebug.png)

If not, check if libusb, openocd and other Linux dependencies listed by Espressif are installed.

Also, make sure you are in the proper group for /dev/tty* access as a user. Often it is 'dialout', but can be different on other distributions:

![TTYACMDialoutGroup](pics/TTYACMDialoutGroup.png)

If not, you can run

```sh
sudo usermod -a -G <group, e.g. dialout> <your username>
```

 and then re-login for it to become effective.

### Serial Print Console

If your driver setup is correct the print console should just work.
If you have multiple devices make sure to select the correct one in VS Code:

![COMPortSelection](pics/COMPortSelection.png)
