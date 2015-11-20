---
layout: guide
title: "Treat Geolocation Data Carefully"
description: "Android and iOS can use GPS to accurately determine location.  Mishandling this GPS data is a privacy concern and may make the user vulnerable to other attacks if the attacker knows their current or past locations. Information about local bluetooth and/or NFC/RFID tags may also leak geolocation information."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 17
order: 206
--- 

## Details

Android and iOS can use GPS to accurately determine location.  Mishandling this GPS data is a privacy concern and may make the user vulnerable to other attacks if the attacker knows their current or past locations. Information about local bluetooth and/or NFC/RFID tags may also leak geolocation information.

## Remediation

Consider implications of using and avoid storing GPS data. For better privacy use the most coarse-grained location services, if possible.  Unless required, do not log or store GPS information. While it may be useful to use GPS for certain applications, it is rarely necessary to log and store the data. Avoiding this prevents many privacy and security issues. GPS positioning information is often cached for a time within the locationd caches on iOS and various caches on Android. Some applications use GPS automatically. One example is the Camera which often geo-tags images. If this is a concern, make sure to strip the EXIF data from the image.

When working in secure locations, remember that GPS data may be reported back to Apple and Google servers to increase accuracy. Both Android and iOS devices are capable of capturing information about nearby access points in range, regardless of whether the device is connected to them. Do not activate GPS in applications that will run at or near secure locations, whose coordinates or wireless network topology should not be reported back to vendors. In addition to this, knowledge of a single access point’s hardware address could be used by an attacker to simulate the secure wireless environment and return GPS coordinates of the environment from Apple or Google.

## References

 * [http://www.sans.org/reading-room/whitepapers/forensics/forensic-analysis-ios-devices-34092](http://www.sans.org/reading-room/whitepapers/forensics/forensic-analysis-ios-devices-34092)

## CWE/OWASP 

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
