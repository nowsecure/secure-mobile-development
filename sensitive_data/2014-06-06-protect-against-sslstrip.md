---
layout: guide
title: "Protect Against SSL Strip"
description: "This MITM attack is difficult to prevent on mobile web apps."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 37
order: 204
--- 

## Details 

This MITM attack is difficult to prevent on mobile web apps. It transparently hijacks HTTP traffic on a network, monitors for HTTPS requests and then eliminates the SSL leaving the client on an unsecured connection.

## Remediation

SSLStrip is a difficult attack to prevent in a web app, but there are several steps which can be taken to mitigate this risk. First, if possible eliminate all HTTP traffic for your secured application. This will not eliminate the risk but help set the proper foundation.

Second, have the client validate that SSL is active. This is straightforward in fully native apps. In mobile web apps, this can be achieved through JavaScript and if an HTTPS connection is not detected, the client can redirect to HTTPS.

A more reliable means of requiring SSL has been designed – the Strict Transport Security HTTP Header. This header causes the browser to require HTTPS for a site once the header has been received. However, browsers are just beginning to implement the Strict Transport Security HTTP Header, and mobile browser support is lagging.

Avoid icons/language that assures user of secure connection but which does not depend on validated HTTPS session. Finally, user education is an important component in reducing the risk of SSLStrip attacks. Reinforce the importance of HTTPS on all user-facing documentation, communication, training, etc.
 
## CWE/OWASP

 * [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * [CWE 757](http://cwe.mitre.org/data/definitions/79.html)
