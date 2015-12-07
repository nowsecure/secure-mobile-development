---
layout: guide
title: "Carefully Manage Debug Logs"
description: "Debug logs are generally designed to be used to detect and correct flaws in an application. These logs can leak sensitive information that may help an attacker create a more powerful attack."
published: 1
categories:
  - caching-and-logging
series:
  name: Caching and Logging
  index: 7
order: 304
--- 

## Details 

Debug logs are generally designed to be used to detect and correct flaws in an application. These logs can leak sensitive information that may help an attacker create a more powerful attack.


## Remediation

Developers should consider the risk that debug logs may pose in a production setting. Generally we recommend that they are disabled in production.

The Android system log typically used by apps for outputting debug messages is a circular buffer of a few kilobytes stored in memory. It may also be possible to recover debug logs from the filesystem in the event of a kernel panic. On device reboot it is cleared, but until then any Android app with the READ_LOGS permission can interrogate the logs. In more recent versions of Android the log files have been more carefully isolated and do not require system level permissions to be requested.

In Android one can also can leverage ProGuard or DexGuard to completely remove the method calls to the Log class in release builds, thus stripping all the calls to Log.d, Log.i, Log.v, Log.e methods.

In *proguard.cfg,* add the following snippet:

```
> -assumenosideeffects class android.util.Log { 
		> public static *** d(...);
		> public static *** v(...);
		> public static *** i(...);
		> public static *** e(...);
> }
```

On iOS disabling the NSLog statements on will remove potentially sensitive information which can be intercepted and as an added benefit may slightly increase the performance of the app. For example, one approach is to define NSLog without a substitution in production builds:

```
> #define NSLog(s,...)

This macro effectively removes all NSLog statements and replaces it with empty text at compilation time.

> NSLog(@”Breakpoint here with data %@”,data.description);

becomes effectively a no-op.

>	;
```

## CWE/OWASP 

 * [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10); [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8)
 * [CWE 215](http://cwe.mitre.org/data/definitions/215.html)
