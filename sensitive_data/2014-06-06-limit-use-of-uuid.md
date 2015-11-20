---
layout: guide
title: "Limit Use of UUID"
description: "Most mobile devices have a unique ID (UUID) created at the time of manufacturing for identification purposes."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 31
order: 205
--- 

## Details 

Most mobile devices have a unique ID (UDID) created at the time of manufacturing for identification purposes. The ability to uniquely identify a device is often important to procure, manage and secure data. Developers quickly adopted the UDID UUID for device identification thus making it a foundation of security for many systems.

Unfortunately, there are several privacy and security issues with this approach. First, many online systems have connected the UUID of a device to an individual user which can enable tracking across applications, even when the user is not logged into the app. This advanced ability to track a user has become a major privacy concern.

Beyond that, apps which identify a person through the UUID risk exposing the data of the previous device owner to a new user. In one instance, after re-setting an iPhone, we were able to gain access to an online music service even though all user data had been erased. This can be both a privacy issue as well as a security threat since it is possible that an attacker may fake a UUID.

Apple has recognized both the privacy and security risks of UUID and has removed developer access. However, developers have used alternative methods, like getting the MAC address of the Wireless network interface or OpenUDID, all methods have been banned at system/API and AppStore review process.

## Remediation

We recommend that developers avoid using any device-provided identifier to identify the device, especially if integral to an implementation of device authentication. Instead, we recommend the creation of an app-unique “device factor” at registration, installation or when the app is first run. This app-unique device factor would be required later along with user authentication to create a session. The device factor could also be used as an additional factor in an encryption routine.

Since it is not relying on predictable, device supplied data, exploitation becomes more difficult. By leveraging a challenge-response approach, the server and device can authenticate each other prior to user authentication. To gain system access an attacker would have to exploit both factors. Developers can also implement a feature where the device factor is reset on the client or server side, forcing a more stringent re-authentication of the user and device.

In order to preserve user privacy and advertising capabilities, Apple recommends using the `advertisingIdentifier` which is a unique identifier that is shared across all apps in the system, but can be reset by the user at any time from the Settings -> Privacy -> Advertising menu.

## References

 * [Unique Identifiers in iOS](https://possiblemobile.com/2013/04/unique-identifiers/)
 
## CWE/OWASP

 * [M5 - Poor Authorization and Authentication](https://www.owasp.org/index.php/Mobile_Top_10_2014-M5)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
