---
layout: guide
title: "Implement Anti-tamper Techniques"
description: "Apps can be tampered with or backdoored and then re-signed by an attacker."
published: 1
categories: 
  - coding-practices
series:
  name: Coding Practices
  index: 32
order: 105
--- 

## Details 

Apps can be tampered with or backdoored and then re-signed by an attacker. Such attacks are often found in the case of popular apps and financial apps. Attackers are known to insert malicious functionality automatically and then publish these malicious versions to third-party markets.

## Remediation

Apps may employ anti-tamper as well as tamper-detection techniques designed to prevent illegitimate applications from running. 

Using checksums, digital signatures and other validation mechanisms on files used in the application can help detect whether data files have been tampered with. Attempts to manipulate the application without preserving a correct checksum can be used to prevent illegitimate execution. Note that such techniques are not foolproof and can be bypassed by a sufficiently motivated attacker. Such techniques are employed to not only increase the time required to breach the application, but also to frustrate an attacker. An application can silently wipe its user data, keys, or other important data wherever tampering is detected to further challenge an attacker. Similarly, applications that have detected tampering can notify an administrator.

On Android, the public key used to sign an app can be read from the app’s certificate and used to verify the application was signed with the developer’s private key. Using the PackageManager class, it’s possible to retrieve the signatures of our application and then compare them with the correct value. If someone has tampered or re-signed the application, the comparison will fail thus detecting the application has been tampered.

## References 

 * Android - [https://gist.github.com/scottyab/b849701972d57cf9562e](https://gist.github.com/scottyab/b849701972d57cf9562e)
 
## CWE/OWASP

 * [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 354](http://cwe.mitre.org/data/definitions/354.html)
