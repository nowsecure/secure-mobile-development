---
layout: guide
title: "Avoid Cached Application Snapshots"
description: "In order to provide the visual transitions in the interface, iOS has been proven to capture and store snapshots (screenshots or captures) as images stored in the file system portion of the device NAND flash. This occurs when an application suspends (rather than terminates), when either the home button is pressed, or a phone call or other event temporarily suspends the application. These images can often contain user and application data. In one published case, they contained the user’s full name, DOB, address, employer, and credit scores."
published: 1
categories:
  - ios
series:
  name: iOS
  index: 18
order: 502
--- 


## Details 

In order to provide the visual transitions in the interface, iOS has been proven to capture and store snapshots (screenshots or captures) as images stored in the file system portion of the device NAND flash. This occurs when an application suspends (rather than terminates), when either the home button is pressed, or a phone call or other event temporarily suspends the application. These images can often contain user and application data. In one published case, they contained the user’s full name, DOB, address, employer, and credit scores.

## Remediation

To protect sensitive data, block caching of application snapshots using API configuration or code. 

When applicationDidEnterBackground: method returns, the snapshot of the application user interface is taken, and it’s used for transition animations and stored in the filesystem. This method should be overridden and all the sensitive information in the user interface should be removed before it returns. This way the snapshot will not contain them.

## References

 * [Managing Your Applications Flow][1]
 
## CWE/OWASP 

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4); [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
 
<!-- Links -->
[1]: https://developer.apple.com/library/iOS/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/ManagingYourApplicationsFlow/ManagingYourApplicationsFlow.html#//apple_ref/doc/uid/TP40007072-CH4-SW47
