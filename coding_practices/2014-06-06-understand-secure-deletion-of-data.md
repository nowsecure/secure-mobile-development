---
layout: guide
title: "Understand Secure Deletion of Data"
description: "On Android calling file.delete() will not securely erase the file and as long as it is not overwritten it can be carved from a physical image of the device."
published: 1
categories:
  - coding-practices
series:
  name: Coding Practices
  index: 36
order: 107
--- 

## Details 

On Android calling file.delete() will not securely erase the file and as long as it is not overwritten it can be carved from a physical image of the device. Traditional approaches to overwriting a file generally do not work on mobile devices due to the aggressive management of the NAND Flash memory.

## Remediation

A developer should assume that any data written to a device can be recovered. In some instances, encryption might add an additional layer of protection.

In addition, while not advisable for most applications, it may be possible to delete a file and then overwrite all available space (create a large file), which would force the NAND Flash to erase all unallocated space. The drawbacks to this technique include wearing out the NAND Flash, causing the app and the entire device to respond slowly, and significant power consumption.

Ideally avoid storing sensitive information on the device where possible. See [BPXX Avoid storing sensitive data].

## References 

 * [General Purpose Cypto](https://developer.apple.com/library/mac/documentation/security/conceptual/cryptoservices/GeneralPurposeCrypto/GeneralPurposeCrypto.html)
 
## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 312](http://cwe.mitre.org/data/definitions/312.html), [313](http://cwe.mitre.org/data/definitions/313.html)
