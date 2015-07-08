---
layout: guide
title: "Increase Code Complexity and Use Obfuscation"
description: "Reverse engineering apps can provide valuable insight into how your app works. By making them more complex internally, an attacker is at a disadvantage to seeing the clear operation of the app, which may reduce the number of attack vectors."
published: 1
categories:
  - coding-practices
series:
  name: Coding Practices
  index: 1
order: 101
--- 

## Details 

Reverse engineering apps can provide valuable insight into how your app works. By making them more complex internally, you put make it more difficult for attackers to see the clear operation of the app, which may reduce the number of attack vectors.

## Remediation

Reverse engineering apps can provide valuable insight into how your app works. By making them more complex internally, you put make it more difficult for attackers to see the clear operation of the app, which may reduce the number of attack vectors.

Reverse engineering of an Android app (.apk file) is achieved rather easily and the internal workings of the application can then be examined. It is recommended that the code be obfuscated to increase the difficulty of examination by malicious users, as described in the Android developer reference.

iOS applications are also susceptible to reverse engineering attacks due to the way they are designed. An app’s classes and protocols are stored within the object file, allowing an attacker to fully map out the application’s design. Objective-C itself is a reflective language, capable of perceiving and modifying its own state; an attacker with the right tools can perceive and modify the state of an application in the same way that the runtime manages the application. Objective-C incorporates a simplistic messaging framework that is very easily traceable and can be manipulated to intercept or even tamper with the runtime of an application. Relatively simple attacks can be used to manipulate the Objective-C runtime to bypass authentication and policy checks, internal application sanity checks, or the kind of logic checks that police the policies of an application.

If the application handles highly sensitive data, consider implementing anti-debug techniques. Various techniques exist which can increase the complexity of reverse engineering your code. One technique is to use C/C++ to limit easy runtime manipulation by the attacker. There are ample C and C++ libraries that are very mature and easy to integrate with Objective-C and Android offers JNI. On iOS consider writing critical portions of code in low-level C to avoid exposure and manipulation by the Objective-C runtime and by Objective-C reverse engineering tools such as class-dump, class-dump-z, Cycript or Frida.

**Restricting debuggers –** An application can specify using a specific system call that the operating system should not permit a debugger to attach to the process. By preventing a debugger from attaching, the capabilities of an attacker to interfere with the low-level runtime are limited. An attacker must first circumvent the debugging restrictions in order to attack the application on a low level. This adds further complexity to an attack. Android applications should have android:debuggable=”false” set in the application manifest to prevent easy run time manipulation by an attacker or malware. On iOS you can make use of the PT_DENY_ATTACH.

**Trace Checking –** An application can determine whether or not it is currently being traced by a debugger or other debugging tool. If being traced, the application can perform any number of possible attack response actions, such as discarding encryption keys to protect user data, notifying a server administrator, or other such type responses in an attempt to defend itself. This can be determined by checking the process status flags or using other techniques like comparing the return value of ptrace attach, checking parent process, blacklist debuggers in the process list or comparing timestamps on different places of the program.

**Optimizations -** To hide advanced mathematical computations and other types of complex logic, utilizing compiler optimizations can help obfuscate the object code so that it cannot easily be disassembled by an attacker, making it more difficult for an attacker to gain an understanding of the particular code. In Android this can more easily be achieved by utilizing natively compiled libraries with the NDK. In addition, using an LLVM Obfuscator or any protector SDK will provide better machine code obfuscation.

**Stripping binaries –** Stripping native binaries is an effective way to increase the amount of time and skill level required of an attacker in order to view the makeup of your application’s low level functions. By stripping a binary, the symbol table of the binary is stripped, so that an attacker cannot easily debug or reverse engineer an application. Stripping binaries does not discard the Objective-C class and object mapping data on iOS. On Android you can reuse techniques used on GNU/Linux systems like `sstrip`ing or using UPX.

iOS binaries in applications distributed in the AppStore are encrypted, adding another layer of complexity. While tools exist to strip the FairPlay digital rights management (DRM) encryption from these binaries, this layer of DRM increases the amount of time and proficiency level required to attack the binary. The encryption used in AppStore application can, however, be stripped by a skilled attacker by dumping the memory from which an application is loaded directly from a device’s memory when run.

## References

 * FairPlay DRM overview on iOS [https://www.theiphonewiki.com/wiki/Copy_Protection_Overview]()
 * Bugging Debuggers on iOS [https://www.theiphonewiki.com/wiki/Bugging_Debuggers]()
 * LLVM-Obfuscator [https://github.com/obfuscator-llvm/obfuscator/wiki]()
 * [http://developer.android.com/guide/publishing/licensing.html#app-obfuscation](http://developer.android.com/guide/publishing/licensing.html#app-obfuscation)
 * Android - ProGuard: [http://proguard.sourceforge.net/](http://proguard.sourceforge.net/) - 
	[http://developer.android.com/tools/help/proguard.html](http://developer.android.com/tools/help/proguard.html) 
 * Android - DexGuard: [http://www.saikoa.com/dexguard](http://www.saikoa.com/dexguard)

## CWE/OWASP 

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 656](http://cwe.mitre.org/data/definitions/656.html)
