---
layout: guide
title: "Fully validate SSL/TLS"
description: "Many apps do not properly validate SSL certificates, leaving them susceptible to man-in-the-middle attacks."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 5
order: 203
--- 

## Details 

Many apps do not properly validate SSL certificates, leaving them susceptible to man-in-the-middle attacks.

## Remediation

Certificates should be fully validated by the client and signed by a trusted root CA. Lower levels of encryption (such as export-grade 40-bit encryption) should be disabled on the server (see Network).

On mobile sites, check HTTPS and host address. Although less tamper-proof than native app code, client-side JavaScript on a mobile site can be used to check for presence of https, proper host URL, and acceptable host IP address. As an improvement, browsers are beginning to implement the Strict Transport Security HTTP Header, which causes the browser to require HTTPS for a site once the header has been received.

In many cases, it is not necessary to use certificates from a public certificate authority, as these were designed for systems where the client did not know whether the system it was connecting to was trusted. Since the majority of applications know exactly where they are connecting to (their backend servers), and inherently trust the infrastructure they are connecting to, it is acceptable (and often more secure) to use a “private” public key infrastructure, separate from public certificate authorities. This way, an attacker would require the private keys from the server side in order to perform a MITM attack or other such types of attacks.

## References

* Android - [http://www.thoughtcrime.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/](http://www.thoughtcrime.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/)

## CWE/OWASP 

 * [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * [CWE 319](http://cwe.mitre.org/data/definitions/319.html)