---
layout: guide
title: "Avoid Storing Cached Camera Images"
description: "Remote-check-deposit apps allow a person to take a picture of a check with their mobile phone's camera and then send the image to their financial institution for deposit into their account."
published: 1
categories:
  - android
series:
  name: Android
  index: 3
order: 610
--- 

## Details 

With remote-check-deposit apps, a person can take a picture of a check with their mobile phone's camera and then send the image to their financial institution for deposit into their account.  Many of these apps will retain the check image (or part of it) in the mobile device's NAND memory even after it is deleted.

## Remediation

Do not transmit a check image using non-volatile storage on the device where check image artifacts may be left behind. One possible alternative is to:
1. Create a SurfaceView that displays a camera preview or live preview of what the camera sensor is seeing
2. Insert and program a button that when pressed returns the camera preview as a pixel array
3. Finally, convert the pixel array to bitmap, compress it to a .jpg, encode it to Base64, and submit it to the remote location

This method will only maintain the image in volatile RAM and prevent the caching of the check image in non-volatile storage.

Specifically with the Android Camera class, the method takePicture can be used specifying a callback when the .jpg is generated using the `Camera.PictureCallback` interface. In particular, we are interested in the method “public void onPictureTaken(byte[] bytes, Camera camera).”

Using this technique it’s possible to use the “bytes” array content, which will contain the photograph in RAM.
 
## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200: Information Exposure](http://cwe.mitre.org/data/definitions/200.html)