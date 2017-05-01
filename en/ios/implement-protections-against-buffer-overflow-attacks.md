# Implement Protections Against Buffer Overflow Attacks

## Details

This best practice covers three iOS code implementations that help developers mitigate the risk of buffer overflow attacks on their app: automatic reference counting (ARC), address space layout randomization (ASLR), and stack-smashing protection.

### Automatic reference counting (ARC)

Automatic Reference Counting (ARC) is a memory management system that handles the reference count of objects automatically at compile time, instead of leaving this task to the developer. This feature was introduced with iOS 5, but it can be backported to previous versions because the operations are performed at compile time.

* The compiler will insert the release and retain calls automatically, making the developer’s life easier, and reduce the risk of introducing vulnerabilities related to the object's memory lifecycle.
* Because the process occurs at compile time it does not introduce any runtime overhead, unlike a garbage collector for example. So there are no obvious drawbacks in switching to ARC.


### Address space layout randomization (ASLR)

ASLR (Address space layout randomization) is a security feature introduced in iOS 4.3 that randomizes how an app is loaded and maintained in memory. ASLR randomizes the address space used in the application, making it difficult to execute malicious code without first causing the application to crash. It also complicates the process of dumping allocated memory of the application. This test checks to see if the application binary was compiled with the -PIE (position-independent executable) flag.

### Stack-smashing protection

When an application is compiled with stack-smashing protection, a known value or "canary" is placed on the stack directly before the local variables to protect the saved base pointer, saved instruction pointer, and function arguments. The value of the canary is verified upon the function return to see if it has been overwritten. The compiler uses a heuristic to intelligently apply stack-smashing protection to a function (typically functions that use character arrays).

## Remediation

**Enable ARC** - Enable ARC in the Xcode project, or migrate existing projects to ARC using the refactoring tool in Xcode.

**Implement full ASLR protection** - Compile the application with support for PIE. PIE can be enabled when compiling by command line with option `-PIE` (on iOS 4.3 or later).

Implement stack-smashing protection - Compile the application with the  `-fstack-protector-all` compiler flag to protect your application against buffer overflow attacks.

## References

  * [Transitioning to ARC Release Notes](https://developer.apple.com/library/content/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html) - https://developer.apple.com/library/content/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html

  * [Address Space Layout Randomization](https://developer.apple.com/library/prerelease/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/BufferOverflows.html#//apple_ref/doc/uid/TP40002577-SW22) - https://developer.apple.com/library/prerelease/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/BufferOverflows.html#//apple_ref/doc/uid/TP40002577-SW22

  * [Other Compiler Flags That Affect Security](https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/BufferOverflows.html#//apple_ref/doc/uid/TP40002577-SW26) - https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/BufferOverflows.html#//apple_ref/doc/uid/TP40002577-SW26

## CWE/OWASP

  * [M7 - Client Code Quality](https://www.owasp.org/index.php/Mobile_Top_10_2016-M7-Poor_Code_Quality)
  * CWE: [CWE-121 - Stack-based Buffer Overflow](https://cwe.mitre.org/data/definitions/121.html), [CWE-200 - Information Exposure](http://cwe.mitre.org/data/definitions/200.html)
