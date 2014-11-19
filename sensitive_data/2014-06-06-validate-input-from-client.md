---
layout: guide
title: "Validate Input From Client"
description: "Even if data is is generated from your app, it is possible for this data to have been intercepted and manipulated."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Senstive Data
  index: 39
order: 213
--- 

## Details 

 Even if data is is generated from your app, it is possible for this data to have been intercepted and manipulated.  This could include attacks that cause the app to crash (generating a key crash log), buffer overflows, SQL Injection, and other attacks. This can easily be enforced in iOS by realizing the methods in the UITextFieldDelegate and taking advantage of the recommendations above.
 
## Remediation

 As with proper web application security, all input from the client should be must be treated as untrusted.  Services must thoroughly filter and validate input from the app and user.  Proper sanitization includes all user input before transmitting and during receipt.

## References 

 * iOS
	[https://developer.apple.com/library/ios/documentation/uikit/reference/UITextFieldDelegate_Protocol/UITextFieldDelegate/UITextFieldDelegate.html](https://developer.apple.com/library/ios/documentation/uikit/reference/UITextFieldDelegate_Protocol/UITextFieldDelegate/UITextFieldDelegate.html)	
 * Android - Content Provider Injection Case of Study - 
	[https://viaforensics.com/mobile-security/ebay-android-content-provider-injection-vulnerability.html](https://viaforensics.com/mobile-security/ebay-android-content-provider-injection-vulnerability.html)
	
## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8)
 * [CWE 79](http://cwe.mitre.org/data/definitions/79.html), [89](http://cwe.mitre.org/data/definitions/89.html), [120](http://cwe.mitre.org/data/definitions/120.html)
 