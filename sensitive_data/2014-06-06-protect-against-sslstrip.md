---
layout: guide
title: "Protect Against SSL Downgrade attacks"
description: "An attacker can transparently swap https sites for their http equivalents, effectively bypassing TLS"
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 37
order: 204
---

## Details

An attacker can transparently swap https sites for their http equivalents, effectively bypassing TLS. As an example, if you vist or type http://google.com, by default you will be redirected to secure, TLS version of the site. An example of this would be a banking webpage serving the landing page in plaintext, only POSTING the login over TLS.  An attacker could rewrite the landing to capture the credentials prior to sending them off to the original endpoint or just redirecting traffic to a attacker controlled server, proxying all traffic.

## Remediation

All traffic, even non-sensitive traffic, should be served over TLS. This prevents any possible downgrade / stripping attacks as you need an initial plaintext 'entrypoint' to accomplish said attack.

Avoid icons/language that assures user of secure connection but which does not depend on validated HTTPS session. User education is an important component in reducing the risk of SSLStrip attacks. Reinforce the importance of HTTPS on all network traffic.

There are currently a few mitigations available for these types of attacks. HSTS (HTTP Strict Transport Security), which requires browser support, is a header included in the response which makes all subsequnt connections that domain use TLS and the certificate that it saw originally. Another mitigation which has been recently put in place on both Android and iOS is to treat non-TLS/plaintext traffic as a developer error.  Android recently added [android:usesCleartextTraffic](https://koz.io/android-m-and-the-war-on-cleartext-traffic/) and iOS 9 and above requires that you manually add exceptions for plaintext traffic.  Further in the future, HTTP/2 is a replacement web protocol that is TLS only, among other features.


## References

* [SSLStrip](http://www.thoughtcrime.org/software/sslstrip/)

## CWE/OWASP

 * [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * [CWE 757](http://cwe.mitre.org/data/definitions/757.html)
