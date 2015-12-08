---
title: "Avoid Intent Sniffing"
description: "When an activity is initiated by another application using a broadcast intent, the data passed in the intent can be read by a malicious app."
layout: guide
published: 1
categories:
  - android
series:
  name: Android
  index: 2
order: 607
--- 

## Details 

When another application initiates activity by sending a broadcast intent, malicious apps can read the data included in the intent. The malicious app can also read a list of recent intents for an application. For example, if an app invokes and passes a URL to the Android web browser, an attacker could sniff that URL.

## Remediation

Do not pass sensitive data between apps using broadcast intents. Instead, use explicit intents.

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 285: Improper Authorization](http://cwe.mitre.org/data/definitions/285.html)
