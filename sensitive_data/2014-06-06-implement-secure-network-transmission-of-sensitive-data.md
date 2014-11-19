---
layout: guide
title: "Implement Secure Network Transmission Of Sensitive Data"
description: "Sensitive data transmitted by apps should be secured with SSL/TLS at a minimum, and with app-layer encryption for passwords and other more sensitive values."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 5
order: 212
--- 

## Details 

App users trust that developers will implement network encryption. And in most cases they have to trust  because unlike web browsers, mobile devices do not show the user when an app is (or is not) using SSL/TLS.

For many years SSL (followed by TLS) has been the standard for encryption of web communications, including the web services that power mobile apps.  But is it still enough? In recent years, breaches of certifying authorities like Diginotar and Comodo exposed many users to false, trusted certificates. The Apple “gotofail” bug further exposed the limits of SSL/TLS reliability for app developers.

Today app providers are expected to use SSL/TLS effectively to secure passwords and private data on the network, and even go further and leverage app-layer encryption to protect their users.

## Remediation

Use SSL/TLS, either with standard trust validation, or for higher security,leverage certificate pinning.

To secure passwords and sensitive data on the network, protecting against flaws and attacks related to SSL/TLS, apps can use asymmetric or symmetric encryption to varying degrees of complexity and security. 


## CWE/OWASP 

 * [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * [CWE-319: Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
 * [CWE-311: Missing Encryption of Sensitive Data](http://cwe.mitre.org/data/definitions/311.html)
