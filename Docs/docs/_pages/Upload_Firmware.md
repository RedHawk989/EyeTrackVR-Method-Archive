---
layout: page
title: Building and uploading the firmware manually
permalink: /building-and-flashing-firmware-manually/
nav_order: 3
parent: Firmware Guide
---

# Building and uploading the firmware manually

Uploading your firmware must initially be done over cable. Once you have the tracker connected to your WiFi after your first firmware update, you can opt to use OTA in the future.

## 1. Connect your tracker to your PC via the programmer.

First, connect your ESP32-Cam to your programmer. In the case of the ESP32-Cam-MB board, it's as simple as sticking it into the socket the way it came in the package and then connecting it to your PC with a micro-USB cable. In some cases, there is a button labeled IOO on the programmer. If that button exists make sure to hold it in while you plug the programmer into your pc, once plugged in you can release the button.

In the case of an FTDI programmer, the steps aren't as easy, so grab [this guide](https://randomnerdtutorials.com/program-upload-code-esp32-cam/) for how to set it up.

## 2. Build your firmware

1. Press the build button at the bottom of Visual Studio Code.

  This builds the firmware, but does not send it to the ESP yet.

   ![img](https://i.imgur.com/EmSkhFp.png)

## 3. Upload your firmware

- If you are using the OTA method, first make sure the tracker you wish to flash is turned on.

- Once the firmware has been built, press the upload button to upload the firmware.

  This sends the firmware to the ESP.
  ![img](https://i.imgur.com/lI3PFVC.png)

{% include custom/alerts/Note.html content="The MB board does the resetting for you, so if you're using the FTDI programmer, follow the guide linked above (the one from randomnerdtutorials)"  %}  

- If the upload is successful, you should get an output that looks like this:

  ![img](https://i.imgur.com/SDQcCr1.png)

Congratulations! You have now successfully uploaded the firmware to your EyeTrackVR Tracker!

If you have trouble with uploading your firmware over cable check the following:

1. Make sure your USB cable from the tracker is plugged firmly into your PC.
2. Make sure that your USB cable is a data and charging cable (it is suggested you try other cables or devices with the cable).
3. Make sure that your drivers are up-to-date.
4. Some ports might not work, try other ones.

Additionally, this can be caused by software hogging COM ports (**VSCode and Cura can be the cause of this**).

## Uploading via OTA

Once you have successfully connected your trackers to your WiFi, you can use OTA to handle all future firmware updates.

1. Retrieve the IP of the tracker you wish to flash. The IP can be found through network monitoring applications, or by viewing tracker output in a serial monitor.
2. In `platformio.ini` file uncomment the following lines in Visual Studio Code by removing the `;`:

```ini
;upload_protocol = espota
;upload_port = 192.168.1.49
```

1. Change the value of upload_port to the IP address retrieved during the first step.
1. Turn the tracker you wish to flash off and then on again.
1. Wait around 5 seconds.
1. Press the upload button to upload the firmware.<br>  
   ![img](https://i.imgur.com/lI3PFVC.png)
1. Repeat for as many trackers as you need.

## Finding the IP address of your tracker

Connect your tracker to your PC and then open a serial monitor in VSC by pressing the "plug" icon.
{% include custom/images/image_2.html url="https://i.imgur.com/dSPSpkY.png" max-width="500" caption="" alt="img" %}

Now, press the restart button on the esp itself.
watch the monitor for output like this:

{% include custom/images/image_2.html url="https://i.imgur.com/PoHP3NC.png" max-width="600" caption="" alt="img" %}

The text, highlighted in green for demonstration, is the stream address of the camera. Take note of this for input into the software.

Keep in mind while testing and getting set up, the ESP can only have one client, to use the camera in the app, make sure you close the browser tab you tested it in.


## Troubleshooting

If you encountered an issue while following these steps check the [FAQ.](https://redhawk989.github.io/EyeTrackVR/faq/)

If you don't find an answer to your question there ask in **#questions** channel in [the discord](https://discord.gg/kkXYbVykZX), we will be happy to help.

*Adapted from the SlimeVR docs, Credit goes to the SlimeVR team [here](https://docs.slimevr.dev/firmware/setup-and-install.html)*
