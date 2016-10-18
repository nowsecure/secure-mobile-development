# Increase Code Complexity and Use Obfuscation

## Details

Reverse engineering apps can provide valuable insight into how your app works. Making your app more complex internally makes it more difficult for attackers to see how the app operates, which can reduce the number of attack vectors.

## Remediation

Reverse engineering apps can provide valuable insight into how your app works. Making your app more complex internally makes it more difficult for attackers to see how the app operates, which can reduce the number of attack vectors.

Reverse engineering an Android app (.apk file) is achieved rather easily and the internal workings of the application can then be examined. Obfuscate the code to make it more difficult for a malicious user to examine the inner-workings of the app as described in the Android developer reference article linked-to below.

iOS applications are also susceptible to reverse engineering attacks due to the way they are designed. An app’s classes and protocols are stored within the object file, allowing an attacker to fully map out the application’s design. Objective-C itself is a reflective language, capable of perceiving and modifying its own state; an attacker with the right tools can perceive and modify the state of an application in the same way that the runtime manages the application. Objective-C incorporates a simplistic messaging framework that is very easily traceable and can be manipulated to intercept or even tamper with the runtime of an application. Relatively simple attacks can be used to manipulate the Objective-C runtime to bypass authentication and policy checks, internal application sanity checks, or the kind of logic checks that police the policies of an application.

If the application handles highly sensitive data, consider implementing anti-debug techniques. Various techniques exist which can increase the complexity of reverse engineering your code. One technique is to use C/C++ to limit easy runtime manipulation by the attacker. There are ample C and C++ libraries that are very mature and easy to integrate with Objective-C, and Android offers JNI. On iOS consider writing critical portions of code in low-level C to avoid exposure and manipulation by the Objective-C runtime or Objective-C reverse engineering tools such as class-dump, class-dump-z, Cycript or Frida.

**Restricting debuggers –** An application can specify using a specific system call to prevent the operating system from permitting a debugger to attach to the process. By preventing a debugger from attaching, an attacker's ability to interfere with the low-level runtime is limited. An attacker must first circumvent the debugging restrictions in order to attack the application on a low level. This adds further complexity to an attack. Android applications should have `android:debuggable=”false”` set in the application manifest to prevent easy runtime manipulation by an attacker or malware. On iOS you can make use of the `PT_DENY_ATTACH`.

**Trace Checking –** An application can determine whether or not it is currently being traced by a debugger or other debugging tool. If it's being traced, the application can perform any number of response actions such as, discarding encryption keys to protect user data, notifying a server administrator, or other such responses in an attempt to defend itself. This can be determined by checking the process status flags or using other techniques like comparing the return value of `ptrace attach`, checking the parent process, blacklisting debuggers in the process list or comparing timestamps on different places of the program.

**Optimizations -** To hide advanced mathematical computations and other types of complex logic, utilizing compiler optimizations can help obfuscate the object code so that it cannot be easily disassembled by an attacker. This makes it more difficult for an attacker to gain an understanding of the particular code. In Android this can be achieved more easily by utilizing natively compiled libraries with the NDK. In addition, using an LLVM Obfuscator or any protector SDK will provide better machine code obfuscation.

**Stripping binaries –** Stripping native binaries is an effective way of increasing the time and skill required of an attacker in order to view the makeup of your application’s low level functions. By stripping a binary, the symbol table of the binary is stripped so that an attacker cannot easily debug or reverse engineer an application. Stripping binaries does not discard the Objective-C class or object-mapping data on iOS. On Android you can reuse techniques used on GNU/Linux systems like `sstrip`ing or using UPX.

The binaries in iOS applications distributed in the App Store are encrypted, adding another layer of complexity. While tools exist to strip the FairPlay digital rights management (DRM) encryption from these binaries, this layer of DRM increases the amount of time and proficiency level required to attack the binary. The encryption used in the App Store application can, however, be stripped by a skilled attacker. The attacker achieves this by dumping the memory from which an application is loaded directly from a device’s memory when it's run.

## References
 * ObjC-Obfuscator [https://github.com/FutureWorkshops/Objc-Obfuscator]()
 * iOS-Class-Guard [https://github.com/Polidea/ios-class-guard]()
 * FairPlay DRM overview on iOS [https://www.theiphonewiki.com/wiki/Copy_Protection_Overview]()
 * Bugging Debuggers on iOS [https://www.theiphonewiki.com/wiki/Bugging_Debuggers]()
 * LLVM-Obfuscator [https://github.com/obfuscator-llvm/obfuscator/wiki]() (for iOS and Android)
 * [http://developer.android.com/guide/publishing/licensing.html#app-obfuscation](http://developer.android.com/guide/publishing/licensing.html#app-obfuscation)
 * Android - ProGuard: [http://proguard.sourceforge.net/](http://proguard.sourceforge.net/) - [http://developer.android.com/tools/help/proguard.html](http://developer.android.com/tools/help/proguard.html)
 * Android - DexGuard: [http://www.saikoa.com/dexguard](http://www.saikoa.com/dexguard)

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE-656: Reliance on Security Through Obscurity](http://cwe.mitre.org/data/definitions/656.html)
