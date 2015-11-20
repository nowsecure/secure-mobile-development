---
layout: guide
title: "Implement PendingIntents Carefully"
description: "PendingIntents allow apps to pass execution to another app which can then call the Intent specified as though they were the originating app."
published: 1
categories:
  - android
series:
  name: Android
  index: 7
order: 605
--- 

## Details 

PendingIntents allow apps to pass execution to another app which can then call the Intent specified as though they were the originating app. This allows external apps to call back to private components.  The external app, if malicious, may try to influence the destination and or data/integrity.

## Remediation

It is best to use PendingIntents as delayed callbacks to private Broadcast Receivers/Activities and explicitly specify the component name as one of your components in the base Intent.

## References 

 * Sample code here [https://gist.github.com/scottyab/d5ab6a284622ebc46d5a](https://gist.github.com/scottyab/d5ab6a284622ebc46d5a)

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 927](http://cwe.mitre.org/data/definitions/927.html)