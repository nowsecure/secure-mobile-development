---
layout: guide
title: "Protect against CSRF with form tokens"
description: "CSRF (Cross-site Request Forgery) relies on known or predictable form values and a logged-in browser session."
published: 1
categories:
  - webviews	
series:
  name: Webviews
  index: 44
order: 402
--- 

## Details 

CSRF (Cross-site Request Forgery) relies on known or predictable form values and a logged-in browser session.

## Remediation

Each form submission should contain a token which was loaded with the form or at the beginning of a user session. Check this token on the server when receiving POST requests to ensure the user originated it. This capability is provided with major web platforms and can be implemented on forms with minimal custom development.

## References 

 * [http://op-co.de/blog/posts/android_ssl_downgrade/](http://op-co.de/blog/posts/android_ssl_downgrade/)

## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 325](http://cwe.mitre.org/data/definitions/325.html)
