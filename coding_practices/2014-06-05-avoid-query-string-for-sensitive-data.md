---
layout: guide
title: "Avoid Query String for Sensitive Data"
description: "A major bank breach was executed with a simple query string modification “attack.” Query string parameters are more visible and can often be unexpectedly cached (web history, webserver or proxy logs, etc.) Using an unencrypted query string for meaningful data should be avoided."
published: 1
categories:
  - coding-practices
series:
  name: Coding Practices
  index: 3
order: 109
---

## Details

A major bank breach was executed with a simple query string modification “attack.” Query string parameters are more visible and can often be unexpectedly cached (web history, webserver or proxy logs, etc.) Using an unencrypted query string for meaningful data should be avoided.  If credentials are transmitted as query string parameters, as opposed to in the body of a POST request, then these are liable to be logged in various places — for example, within the user’s browser history, within the web server logs, and within the logs of any reverse proxies employed within the hosting infrastructure. If an attacker succeeds in compromising any of these resources, then she may be able to escalate privileges by capturing the user credentials stored there.

## Remediation 

Use secure POST to send user data, with XSRF token protection. POST data is not logged by default in areas where query string data can be found.  Whether POST or GET, temporary session cookies should be used. Encrypting data using a non-zero initialization vector and temporary session keys can also help prevent a replay attack. If necessary, query string data can be encrypted using a temporary session key negotiated between hosts using secure algorithms, such as Diffie-Hellman.

## References

Pinto, Marcus (2007). The Web Application Hacker’s Handbook: Discovering and Exploiting Security Flaws (Kindle Locations 2813-2816). Wiley. Kindle Edition.

## CWE/OWASP 

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2), [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 598](http://cwe.mitre.org/data/definitions/316.html)
