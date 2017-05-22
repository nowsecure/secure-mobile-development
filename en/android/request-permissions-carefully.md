# 7.13 Request Android permissions carefully

## Details

Android uses permissions to manage access to data and APIs.

Misconfigured or over-privileged apps can sometimes open the door to attackers by granting unintended permissions.

One of many examples of exploiting permissions is the “confused deputy” attack. In the confused deputy attack, an app that doesn’t have explicit permission to access a file requests the file via another service that has permission. The system uses that service’s permission to allow access to the file despite the app not having proper permission to access it.

## Remediation

Newer Android versions support runtime permissions, which allow developers to request the permissions from the user when they are needed. This has a number of positive impacts to security including delaying the granting of so called [dangerous permissions](https://developer.android.com/guide/topics/security/permissions.html#normal-dangerous).

* Only request the permissions needed for your application to function. Note that even if you request minimum permissions, a logic flaw may still exist that, if exploited, can make your app a confused deputy. 
* In general it is best to only request the permissions needed for the app to function, and as of Android 6.0 (Marshmallow), [runtime permissions](https://developer.android.com/training/permissions/requesting.html) were introduced to help users and developers agree on acceptable permissions.
* Make sure to provide context to users about why the permission is needed at runtime.

While runtime permissions can complicate development, with newer Android versions they aren't optional. They can, however, be managed more conveniently with third-party libraries and Java annotations (see [PermissionsDispatcher](https://github.com/hotchemi/PermissionsDispatcher) and [Dexter](https://github.com/Karumi/Dexter).

Granting dangerous permissions to your app can make it more of a target. Requesting/gaining the permission only if the user actually needs the functionality can help reduce the specific targeting of your app, or otherwise make it harder to execute an attack.

## CWE/OWASP

* OWASP Mobile Top 10: [M1 - Improper Platform Usage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M1-Improper_Platform_Usage)
* CWE: [CWE-441 - Unintended Proxy or Intermediary ('Confused Deputy')](https://cwe.mitre.org/data/definitions/441.html)
