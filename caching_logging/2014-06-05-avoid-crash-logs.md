---
layout: guide
title: "Avoid Crash Logs"
description: "If an app crashes, the resulting log can provide valuable info to an attacker."
published: 1
categories:
  - caching-and-logging
series:
  name: Caching and Logging
  index: 4
order: 302
--- 

## Details 

If an app crashes, the resulting log can provide valuable info to an attacker.

## Remediation

Ensure apps are built without warnings and are thoroughly tested to avoid crashes. This is certainly always the goal and worth mentioning due to the value of a crash log.  Consider disabling NSAssert for iOS. This setting will cause an app to crash immediately if an assertion fails. It is more graceful to handle the failed assertion than to crash and generate the crash log. Also, avoid sending crash logs over the network in plaintext.

## CWE/OWASP 

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 215](http://cwe.mitre.org/data/definitions/215.html)

