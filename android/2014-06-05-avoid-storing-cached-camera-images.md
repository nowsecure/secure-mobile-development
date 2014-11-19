---
layout: guide
title: "Avoid Storing Cached Camera Images"
description: "Remote check deposit apps allow the user to take a picture of a check using the phone’s camera and send it off to the financial institution to deposit in an account."
published: 1
categories:
  - android
series:
  name: Android
  index: 3
order: 610
--- 

## Details 

Remote check deposit apps allow the user to take a picture of a check using the phone’s camera and send it off to the financial institution to deposit in an account.  Many of these apps leave part  or all of an image of the check on the phone’s NAND memory even after it is deleted.

## Remediation

It is recommended that a different approach be used to avoid leaving check image artifacts on non-volatile storage in the device. One possible approach on Android is to create a SurfaceView and have it display a Camera Preview, or a live preview of what the camera is seeing.  Then, insert and program a button that when pressed returns the Camera Preview as a pixel array. This can then be converted to a bitmap, compressed to JPG, base64 encoded and submitted to the the remote location. This data flow maintains the image only in in volatile RAM to avoid the possibility of an image being cached to non-volatile storage.

Specifically with the Android Camera class, the method takePicture can be used specifying a callback when the JPEG is generated using the Camera.PictureCallback interface. In particular we are interested in the method “public void onPictureTaken(byte[] bytes, Camera camera).”

Using this technique it’s possible to use the “bytes” array content, which will contain the photograph in RAM.
 
## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)