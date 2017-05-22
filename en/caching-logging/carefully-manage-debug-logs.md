# Carefully Manage Debug Logs

## Details

Debug logs are generally designed to be used to detect and correct flaws in an application. These logs can leak sensitive information that may help an attacker create a more powerful attack.


## Remediation

Developers should consider the risk that debug logs may pose in a production setting. Generally we recommend that they are disabled in production.

### Android
The Android system log typically used by apps for outputting debug messages is a circular buffer of a few kilobytes stored in memory. It may also be possible to recover debug logs from the filesystem in the event of a kernel panic. On device reboot it is cleared, but until then any Android app with the READ_LOGS permission can interrogate the logs -- *only applicable to Android 4.1 - 4.3.1 and earlier*. In more recent versions of Android the log files have been more carefully isolated and do not require system level permissions to be requested. However, certain original equipment manufacturers (OEMs) add customizations to Android that expose full system logs to other apps on a device without the need for system-level permissions. Therefore, we recommend that Android developers take additional remediation actions.

#### Remove method calls to the Log class in release builds

Use ProGuard or DexGuard to completely remove the method calls to the Log class in release builds, thus stripping all the calls to Log.d, Log.i, Log.v, Log.e methods.

In *proguard.cfg,* add the following snippet:

```
> -assumenosideeffects class android.util.Log {
		> public static *** d(...);
		> public static *** v(...);
		> public static *** i(...);
		> public static *** e(...);
> }
```
#### Set the “android:debuggable” flag to “false” in production builds
Android 7 (API level 24) gives developers the ability to configure a debug-only certificate authority (CA). The debug-only CA will only be trusted by the app when the app’s debug flag, `android:debuggable`, is set to true. By default, the `android:debuggable` flag is set to false. For quality assurance and other testing purposes, the app’s debug flag, `android:debuggable`, can be set to true so that the app will function in staging environments. Prior to releasing an app to production, ensure that the `android:debuggable` flag is set to false or removed.

### iOS
On iOS disabling the NSLog statements on will remove potentially sensitive information which can be intercepted and as an added benefit may slightly increase the performance of the app. For example, one approach is to define NSLog without a substitution in production builds:

```
> #define NSLog(s,...)

This macro effectively removes all NSLog statements and replaces it with empty text at compilation time.

> NSLog(@”Breakpoint here with data %@”,data.description);

becomes effectively a no-op.

>	;
```

## CWE/OWASP

 * OWASP Mobile Top 10: [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage), [M7 - Client Code Quality](https://www.owasp.org/index.php/Mobile_Top_10_2016-M7-Poor_Code_Quality)
 * CWE: [CWE 215 - Information Exposure Through Debug Information](http://cwe.mitre.org/data/definitions/215.html)
