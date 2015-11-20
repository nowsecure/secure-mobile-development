---
layout: guide
title: "Use Automatic Reference Counting (ARC)"
description: "Automatic Reference Counting is a memory management system that takes care at compile time of the reference count of objects automatically, instead of leaving this task to the developer."
published: 1
categories:
  - ios	
series:
  name: iOS
  index: 48
order: 503
--- 

## Details 

Automatic Reference Counting is a memory management system that takes care at compile time of the reference count of objects automatically, instead of leaving this task to the developer. This feature was introduced with iOS 5, but it can be backported to previous versions because the operations are performed at compile time.

The compiler will insert the release and retain calls automatically, making the developer’s life easier, and eliminating risks of introducing vulnerabilities related to the object's memory lifecycle.

The process is completely done at compile time, so it does not introduce any runtime overhead, like a garbage collector for example, so there are no drawbacks for developers switching to Automatic Reference Counting.

## Remediation

Enable ARC in the Xcode project, or migrate existing projects to ARC with the Refactoring tool provided by Apple in Xcode that helps the developer in the process.

## References

 * [https://developer.apple.com/library/ios/releasenotes/objectivec/rn-transitioningtoarc/introduction/introduction.html](https://developer.apple.com/library/ios/releasenotes/objectivec/rn-transitioningtoarc/introduction/introduction.html)

## CWE/OWASP

 * [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
 
 
