# Securely Store Sensitive Data in RAM

Oftentimes, iOS developers will store application settings in plist files which can be compromised in some situations.

## Details

When an application is in use, user- or application-specific data may be stored in RAM and not properly cleared when the user logs out or the session times out. Because Android stores an application in memory (even after use) until the memory is reclaimed, encryption keys may remain in memory. An attacker who finds or steals the device can attach a debugger and dump the memory from the application, or load a kernel module to dump the entire contents of RAM.

When managing passwords and other sensitive information, applications will keep that information in memory, even if the buffer is freed for some time. This can be a security problem if the application is prone to buffer overflow, format string, data leak and other vulnerabilities, which might allow an attacker to dump the memory of the process in order to recover that sensitive information.

## Remediation

Do not keep sensitive data (e.g., encryption keys) in RAM longer than required. Nullify any variables that hold keys after use. Avoid using immutable objects for sensitive keys or passwords such as in Android `java.lang.String` and use char array instead. Even if references to immutable objects are removed or nulled, they may remain in memory until garbage collection occurs (which cannot be forced by the app).

This can be only done by low-level languages because the compilers and just-in-time virtual machines will ignore those operations for performance reasons if the optimization routines detect that the buffer is no longer used after being overwritten.

There are some recommendations in order to clear those buffers bypassing the compiler optimizations, but they are all toolchain, language and platform dependant.

## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * [CWE-316: Cleartext Storage of Sensitive Information in Memory](http://cwe.mitre.org/data/definitions/316.html)
 * [CWE-200: Information Exposure](http://cwe.mitre.org/data/definitions/200.html)
 * [CVE-2014-0160 Heartbleed](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0160)
