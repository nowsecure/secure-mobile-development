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

On Android calling file.delete() will not securely erase the file and as long as it is not overwritten it can be carved from a physical image of the device. Traditional approaches to wipe a file generally do not work on mobile devices due to the aggressive management of the NAND Flash memory.

When managing passwords and other sensitive information, applications will kept that information in memory, even if the buffer is freed for some time. This can be a security problem if the application is vulnerable to buffer overflows, format string, data leaks vulnerabilities that can lead an attacker to dump the memory of the process in order to recover that sensible information.

## Remediation

A developer should assume that any data written to a device can be recovered. In some instances, encryption might add an additional layer of protection.

In addition, while not advisable for most applications, it may be possible to delete a file and then overwrite all available space (create a large file), which would force the NAND Flash to erase all unallocated space. The drawbacks to this technique include wearing out the NAND Flash, causing the app and the entire device to respond slowly, and significant power consumption.

Ideally avoid storing sensitive information on the device where possible. See [BPXX Avoid storing sensitive data].

Encrypting the sensitive data stored in files and rewriting the contents of the file and syncing before deleting can be useful in some situations, but, as described above, are not fully reliable solutions to the problem.

In order to protect sensitive data in memory, the developer must ensure that all the buffers containing sensitive information should be cleared right before being freed. This can be only done by low-level languages because the compilers and just-in-time virtual machines will ignore those operations for performance reasons if the optimization routines detect that the buffer is no longer used after being overwritten.

There are some recommendations in order to clear those buffers bypassing the compiler optimizations, but they are all pretty compiler, language and platform dependant.


## References 

 * [General Purpose Cypto](https://developer.apple.com/library/mac/documentation/security/conceptual/cryptoservices/GeneralPurposeCrypto/GeneralPurposeCrypto.html)
 
## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 312](http://cwe.mitre.org/data/definitions/312.html), [313](http://cwe.mitre.org/data/definitions/313.html)
