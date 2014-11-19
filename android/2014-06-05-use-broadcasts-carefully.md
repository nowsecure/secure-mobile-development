---
layout: guide
title: "Use Broadcasts carefully"
description: "When sending a broadcast Intent, if no permission is set then any unprivileged app can receive the Intent unless it has an explicit destination. "
published: 1
categories:
  - android
series:
  name: Android
  index: 10
order: 604
--- 

## Details 

When sending a broadcast Intent, if no permission is set then any unprivileged app can receive the Intent unless it has an explicit destination.  There is no restriction on a malicious developer creating an app with the exact same component name as a legitimate component, and as long as the namespace is not in use already the malicious app will install.

## Remediation

Use permissions to protect Intents in your application and consider that if you are sending sensitive information via a broadcast Intent to a 3rd party component then the component could have been replaced by a malicious install.

## References 

 * [https://developer.android.com/training/articles/security-tips.html#Permissions](https://developer.android.com/training/articles/security-tips.html#Permissions)
 * [http://shop.oreilly.com/product/0636920022596.do](http://shop.oreilly.com/product/0636920022596.do)

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 925](http://cwe.mitre.org/data/definitions/925.html)
