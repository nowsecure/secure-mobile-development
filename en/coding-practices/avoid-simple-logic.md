# Avoid Simple Logic

## Details

Simple logic tests in code are more susceptible to attack. Example:

```
if sessionIsTrusted == 1
```

This is a simple logic test and if an attacker can change that one value, they can circumvent the security controls. Apple iOS has been attacked using this type of weakness and Android apps have had their Dalvik binaries patched to circumvent various protection mechanisms. These logic tests are easy to circumvent on many levels. On an assembly level, an attacker can attack an iOS application using only a debugger to find the right CBZ (compare-and-branch-on-zero) or CBNZ (compare-and-branch-on-nonzero) instruction and reverse it. This can be performed in the runtime as well by simply traversing the object’s memory address and changing its instance variable as the application runs. On Android, the application can be decompiled to SMALI and the branch condition patched before recompiling.

## Remediation

Consider a better programming paradigm, where privileges are enforced by the server when the session is not trusted, or by preventing certain data from being decrypted or otherwise available until the application can determine that the session is trusted using challenge/response, OTP, or other forms of authentication. In addition, it is recommended to declare all sanity check functions static inline. With this approach they are compiled inline, making it more difficult to patch out (i.e. an attacker cannot simply override a function or patch one function). This technique would require the attacker to seek out and patch every instance of the check from the application, increasing the required complexity of an attack. For highly sensitive apps, more sophisticated approaches founded in secure coding principles may be worth further investigation. Integrating techniques such as encryption, timed callbacks and flow-based programming can add complexity for an attacker.

In the same vein, simple logic variables stored in an object can be easily manipulated by an attacker. Example:

```
session.trusted = TRUE
```

Such values can be both read and written to by an attacker within the instance of a class currently in use by the application. On iOS by manipulating the Objective-C runtime, these variables can be manipulated so that the next time they are referenced by the application, any manipulated values will be read instead.

## CWE/OWASP

 * [M8 - Code Tampering](https://www.owasp.org/index.php/Mobile_Top_10_2016-M8-Code_Tampering), [M9 - Reverse Engineering](https://www.owasp.org/index.php/Mobile_Top_10_2016-M9-Reverse_Engineering)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
