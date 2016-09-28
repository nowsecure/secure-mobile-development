---
layout: guide
title: "Protect Internal Resources"
description: "Resources for internal use such as administrator login forms frequently leverage authentication that is not resistant to brute force."
published: 1
categories:
  - servers	
series:
  name: Servers
  index: 46
order: 705
--- 

## Details 

Resources for internal use such as administrator login forms frequently leverage authentication that is not resistant to brute force. For example HTTP or forms authentication without lockout. Compromise of administration or other internal resources can lead to extensive data loss and other damage.

## Remediation

Such resources should be blocked from external access.   Any resource that does not require public Internet access should be restricted using firewall rules and network segmentation. If a login page, admin area or other resource is accessible externally, assume it will be discovered by malicious users and attacked by brute force.

## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 200 - Multiple CWE's](http://cwe.mitre.org/data/definitions/200.html)