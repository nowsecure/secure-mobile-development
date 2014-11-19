---
layout: guide
title: "Implement Enhanced / Two-Factor Authentication"
description: "Weak passwords do not offer significant protection."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 33
order: 209
--- 

## Details 

Apps can be tampered with or backdoored and then re-signed by an attacker. Such attacks are often found in the case of popular apps and financial apps. Attackers are known to insert malicious functionality automatically and then publish these malicious versions to third-party markets.

## Remediation

A password should not be simplistic. Support or require complex passwords, including length of at least 6 alphanumeric characters (more is always stronger). Adding a secret word/icon selection which user does not create helps protect users in case their (same) password was compromised on a different service.

In some cases a username and password does not provide sufficient security for a mobile app. When sensitive data or transactions are involved, implement two-factor authentication. This may not be feasible for every login but can be used at intervals or when accessing selected functions. Step-up authentication allows normal access to non-transactional areas and requires a second layer of authentication for sensitive functions.

Options for enhanced authentication include:

 * Additional secret word/icon.*
 
 * Additional code provided by SMS or email -- but be aware that an attacker will likely have access to both on a stolen device.*
 
 * Password plus additional user-known value, for example user-selected personal factor.*
 
 * Security questions/answer, set by user in advance (e.g. during registration).*

For highest security, the use of one-time passwords (OTP) requires the user of the application to not only possess the correct credentials, but also a physical token containing the one time password.

## CWE/OWASP 

 * [M5 - Poor Authorization and Authentication](https://www.owasp.org/index.php/Mobile_Top_10_2014-M5)
 * [CWE 308](http://cwe.mitre.org/data/definitions/308.html)
