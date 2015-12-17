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

An attacker can transparently swap HTTPS sites for their HTTP equivalents, effectively bypassing TLS. For example, if you visit or type http://google.com, by default you will be redirected to a secure, TLS version of the site. An example of this would be a banking webpage serving the landing page in plaintext, only POSTING the login over TLS.  An attacker could rewrite the landing page to capture the credentials prior to sending them off to the original endpoint or just redirect traffic to an attacker-controlled server, proxying all traffic.

## Remediation

All traffic, even non-sensitive traffic, should be served over TLS. This prevents any possible downgrading/stripping attacks as an attacker needs an initial plaintext 'entry point' to accomplish said attack.

Avoid icons or verbiage within the UI that assures users of a secure connection when said connection does not depend on a validated HTTPS session. User education is an important component in reducing the risk of SSL-strip attacks. Use alerts and text within the UI to reinforce to users the importance of network traffic being protected by HTTPS.

There are currently a few mitigations available for these types of attacks. HSTS (HTTP Strict Transport Security), which requires browser support, is a header included in the response which makes all subsequent connections to that domain use TLS and the certificate that it saw originally. Another mitigation which has been recently put in place on both Android and iOS is to treat non-TLS/plaintext traffic as a developer error.  Android recently added [android:usesCleartextTraffic](https://koz.io/android-m-and-the-war-on-cleartext-traffic/), and iOS 9 and above require that you manually add exceptions for plaintext traffic.  Further in the future, HTTP/2 is a replacement web protocol that is TLS only, among other features.


## References

* [SSLStrip](http://www.thoughtcrime.org/software/sslstrip/)

## CWE/OWASP

 * [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * [CWE-757: Selection of Less-Secure Algorithm During Negotiation ('Algorithm Downgrade')](http://cwe.mitre.org/data/definitions/757.html)


