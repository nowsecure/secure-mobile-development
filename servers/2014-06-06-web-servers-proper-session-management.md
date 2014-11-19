---
layout: guide
title: "Use Proper Session Management"
description: "Sessions for users are maintained on most apps via a cookie, which can be vulnerable."
published: 1
categories:
  - servers
series:
  name: servers
  index: 40
order: 703
--- 

## Details 

Sessions for users are maintained on most apps via a cookie, which can be vulnerable.


## Remediation

Web languages (e.g. Java, .NET) offer session management, which is well-developed and security tested. Keep server software up-to-date with security patches. Rolling your own session management is more risky and undertaken only with proper expertise.  Ensure the size of the session cookie is sufficient. Short or predictable session cookies make it possible for an attacker to predict, highjack or perform other attacks against the session. Use high-security settings in session configuration.


## CWE/OWASP

 * [M9 - Improper Session Handling](https://www.owasp.org/index.php/Mobile_Top_10_2014-M9)
 * [CWE 613](http://cwe.mitre.org/data/definitions/613.html)