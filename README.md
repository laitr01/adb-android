# Android Debug Bridge (adb)
Android Debug Bridge (adb) is a versatile command-line tool that lets you communicate with a device. 
+ installing and debugging apps
+ access to a Unix shell that you can use to run a variety of commands on a device. 
+ client-server program that includes three components:

      A client, which sends commands. The client runs on your development machine.
      A daemon (adbd), which runs commands on a device. The daemon runs as a background process on each device.
      A server, which manages communication between the client and the daemon. 
      
## Connect to a device over Wi-Fi

1. Connect your Android device and adb host computer to a common Wi-Fi network accessible to both. 
2. Connect the device to the host computer with a USB cable.
3. Set the target device to listen for a TCP/IP connection on port 5555.

                `adb tcpip 5555`

4. Disconnect the USB cable from the target device.
5. Find the IP address of the Android device. For example, on a Nexus device, you can find the IP address at Settings > About tablet (or About phone) > Status > IP address. Or, on a Wear OS device, you can find the IP address at Settings > Wi-Fi Settings > Advanced > IP address.
6. Connect to the device by its IP address.

  `adb connect device_ip_address`

7. Confirm that your host computer is connected to the target device:
```
$ adb devices
List of devices attached
device_ip_address:5555 device
```

If the adb connection is ever lost:

Make sure that your host is still connected to the same Wi-Fi network your Android device is.
Reconnect by executing the adb connect step again.
Or if that doesn't work, reset your adb host:

`adb kill-server`

Then start over from the beginning.

## Send commands to a specific device

In the following example, the list of attached devices is obtained, and then the serial number of one of the devices is used to install the helloWorld.apk on that device.

        $ adb devices
        List of devices attached
        emulator-5554 device
        emulator-5555 device

        $ adb -s emulator-5555 install helloWorld.apk

## Install an app
```
adb install path_to_apk
```
## Copy files to/from a device

-> To copy a file or directory and its sub-directories from the device, do the following:
```
adb pull remote local
```
-> To copy a file or directory and its sub-directories to the device, do the following:
```
adb push local remote
```
-> Replace local and remote with the paths to the target files/directory on your development machine (local) and on the device (remote). For example:
```
adb push foo.txt /sdcard/foo.txt
```
## Stop the adb server
```
adb kill-server
```

## Issue shell commands
+ Call activity manager (am)
```
adb shell am start -a android.intent.action.VIEW
```
