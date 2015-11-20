---
title: "Avoid Intent Sniffing"
description: "When an activity is started by another application using a Broadcast Intent the data passed in the Intent can be read by a malicious app."
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

When an activity is started by another application using a Broadcast Intent, the data passed in the Intent can be read by a malicious app. The malicious app can also read a list of recent Intents for an application. For example, when the Android Web browser is invoked by an app which passes it a URL, that URL can be sniffed.

## Remediation

It is recommended that sensitive data should not be passed between apps using Broadcast Intents. Instead use explicit intents.

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 285](http://cwe.mitre.org/data/definitions/285.html)
