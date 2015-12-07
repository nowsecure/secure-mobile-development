---
layout: guide
title: "Test Third-Party libraries"
description: "Developers rely heavily on third-party libraries. It is important to thoroughly probe and test this as you test your code.  Third-party libraries can contain vulnerabilities and weaknesses. Many developers assume third-party libraries are well-developed and tested, however, issues can and do exist in their code."
published: 1
categories:
  - coding-practices
series:
  name: Coding Practices
  index: 16
order: 104
--- 

## Details 

Developers rely heavily on third-party libraries. It is important to thoroughly probe and test this as you test your code.  Third-party libraries can contain vulnerabilities and weaknesses. Many developers assume third-party libraries are well-developed and tested, however, issues can and do exist in their code.

## Remediation

Security auditing must thoroughly test third-party libraries and functionality as well. This should include core iOS and Android code/libraries. Upgrading to a new version of a third-party library (or OS version) should be treated as version of your app. An updated third-party library (or new OS version) can contain new vulnerabilities or expose issues in your code. They should be tested just like you test new code for your app. On iOS, statically compile third-party libraries to avoid LD_PRELOAD attacks; in such attacks a library and its functions can be swapped out for an attacker’s library with functions replaced with malicious code. 

## CWE/OWASP 

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8)
 * [CWE 829](http://cwe.mitre.org/data/definitions/829.html)