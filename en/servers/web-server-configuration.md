---
layout: guide
title: "Implement Proper Web Server Configuration"
description: "Certain settings on a web server can increase security."
published: 1
categories:
  - servers
series:
  name: servers
  index: 42
order: 701
--- 

## Details 

Certain settings on a web server can increase security. One commonly overlooked vulnerability on a web server is information disclosure. Information disclosure can lead to serious problems, because every piece of information attackers can gain from a server makes staging an attack easier.

## Remediation

A simple way to reduce information disclosure is to disable verbose errors. Verbose errors can be useful in a development environment, but in a production environment can leak critical information such as web framework information and versions. Attackers can use this information to target attacks that are designed to exploit implementation-specific flaws.

Another simple way to reduce information disclosure is to return the minimum amount of information in server responses. By default, Apache will return its version number, the OS it is running on, and the plugins running. By changing a single line in the configuration file, this can be pared down to only disclosing that the server is running Apache with no effect on functionality.

One configuration change in servers that can greatly improve security is to change any default directories. Attackers frequently search the Internet for sites with “low-hanging fruit,” such as default logins, easily guessable admin interfaces, and simple naming schemes for “hidden” directories. It is a good policy to obfuscate the locations of any sensitive pages on a server that need to be web-accessible.

Administration or other restricted areas should not be publicly web-accessible unless absolutely necessary, and must be resistant to brute force attacks. HTTP authentication or forms authentication without lockout protection can (and will) be attacked by brute force.
 
## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 203](http://cwe.mitre.org/data/definitions/203.html)
