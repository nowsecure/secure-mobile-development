---
title: "Implement intents carefully"
description: "Intents are used for inter-component signalling and can be used"
layout: guide
published: 1
categories:
  - android
order: 602
---

## Details 

Intents are used for inter-component signaling and can be used

 * *To start an Activity, typically opening a user interface for an app*
 * *As broadcasts to inform the system and apps of changes*
 * *To start, stop, and communicate with a background service*
 * *To access data via ContentProviders*
 * *As callbacks to handle events*

Improper implementation could result in data leakage, restricted functions being called and program flow being manipulated.

## Remediation

 * Components accessed via Intents can be public or private. The default is dependent on the intent-filter and it is easy to mistakenly allow the component to be or become public. It is possible to set component as android:exported=false in the app’s Manifest to prevent this.
 
 * Public components declared in the Manifest are by default open so any application can access them. If a component does not need to be accessed by all other apps, consider setting a permission on the component declared in the Manifest.

 * Data received by public components cannot be trusted and must be scrutinized.

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 927](http://cwe.mitre.org/data/definitions/316.html)
