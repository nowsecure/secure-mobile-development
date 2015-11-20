---
layout: guide
title: "Institute Local Session Timeout"
description: "Mobile devices are frequently lost or stolen, and an attacker may leverage an app to access sensitive data, execute transactions, or research a device owner’s accounts."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 6
order: 208
--- 

## Details 

Mobile devices are frequently lost or stolen, and an attacker may leverage an app to access sensitive data, execute transactions, or research a device owner’s accounts.

## Remediation

Any time the app is not actively utilized for more than 5 minutes, the active session should terminate and the user should be required to re-enter credentials.  When an application’s session is timed out, the application should also discard and clear all memory associated with the user data, and any master keys used to decrypt data. A skilled attacker operating on a stolen device could potentially steal this data from memory if it is not cleared.

## CWE/OWASP 

 * [M9 - Improper Session Handling](https://www.owasp.org/index.php/Mobile_Top_10_2014-M9)
 * [CWE 613](http://cwe.mitre.org/data/definitions/613.html)
 
