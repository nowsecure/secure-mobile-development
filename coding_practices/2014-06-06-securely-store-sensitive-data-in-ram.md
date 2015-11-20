---
layout: guide
title: "Securely Store Sensitive Data in RAM"
description: "iOS developers often store application settings in plist files which can be compromised in some situations."
published: 1
categories:
  - coding-practices
series:
  name: Coding Practices
  index: 35
order: 106
--- 

## Details 

During application use, user or application specific data could be stored in RAM and not cleared properly upon user logout or session timeout. On Android, because an application stays in memory after use until the memory needs to be reclaimed, encryption keys can linger in the background. An attacker who finds or steals the device can attach a debugger and dump the memory from the application, or load a kernel module to dump the entire contents of RAM.

When managing passwords and other sensitive information, applications will kept that information in memory, even if the buffer is freed for some time. This can be a security problem if the application is vulnerable to buffer overflows, format string, data leaks vulnerabilities that can lead an attacker to dump the memory of the process in order to recover that sensible information.

## Remediation

When using sensitive data such as encryption keys, do not keep them in RAM longer than required. Variables holding keys should be nullified after use. Avoid using immutable objects for sensitive keys/passwords such as in Android java.lang.String and favour char array instead. This is because even when references to immutable objects are removed/nulled they made still be present in memory until garbage collection which cannot be forced by the app.

This can be only done by low-level languages because the compilers and just-in-time virtual machines will ignore those operations for performance reasons if the optimization routines detect that the buffer is no longer used after being overwritten.

There are some recommendations in order to clear those buffers bypassing the compiler optimizations, but they are all toolchain, language and platform dependant.

## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 316](http://cwe.mitre.org/data/definitions/316.html), [200](http://cwe.mitre.org/data/definitions/200.html)
 * [CVE-2014-0160 Heartbleed](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0160)
