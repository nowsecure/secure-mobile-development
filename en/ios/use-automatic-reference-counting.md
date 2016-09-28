---
layout: guide
title: "Use Automatic Reference Counting (ARC)"
description: "Automatic Reference Counting is a memory management system that handles the reference count of objects automatically at compile time, instead of leaving this task to the developer."
published: 1
categories:
  - ios	
series:
  name: iOS
  index: 48
order: 503
--- 

## Details 

Automatic Reference Counting (ARC) is a memory management system that handles the reference count of objects automatically at compile time, instead of leaving this task to the developer. This feature was introduced with iOS 5, but it can be backported to previous versions because the operations are performed at compile time.

The compiler will insert the release and retain calls automatically, making the developer’s life easier, and reduce the risk of introducing vulnerabilities related to the object's memory lifecycle.

Because the process occurs at compile time it does not introduce any runtime overhead, unlike a garbage collector for example. So there are no obvious drawbacks in switching to ARC.

## Remediation

Enable ARC in the Xcode project, or migrate existing projects to ARC using the refactoring tool in Xcode.

## References

 * [https://developer.apple.com/library/ios/releasenotes/objectivec/rn-transitioningtoarc/introduction/introduction.html](https://developer.apple.com/library/ios/releasenotes/objectivec/rn-transitioningtoarc/introduction/introduction.html)

## CWE/OWASP

 * [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE-200: Information Exposure](http://cwe.mitre.org/data/definitions/200.html)