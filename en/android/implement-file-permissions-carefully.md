# 7.1 Implement File Permissions Carefully

## Details

World readable files can act as a vector for your program to leak sensitive information. World writeable files may expose your app by letting an attacker influence its behavior by overwriting data that is read by your app from storage.  Examples include settings files and stored login information.

## Remediation

* Do not create files with permissions of MODE_WORLD_READABLE or MODE_WORLD_WRITABLE unless it is required as any app would be able to read or write the file even though it may be stored in the app’s private data directory. _Note: Both of these modes were deprecated in Android API level 17 (see [http://developer.android.com/reference/android/content/Context.html](http://developer.android.com/reference/android/content/Context.html)). At this time, use of either mode will trigger a `SecurityException` though the restriction is not yet fully enforced._

* Do not use modes such as 0666, 0777, and 0664 with the `chmod` binary or `syscalls` accepting a file mode (`chmod`, `fchmod`, `creat`, etc) _Note: Android 7.0 (API level 24) and higher sets all private directories (`data/data`) to restricted access -- mode 0700 (see [https://developer.android.com/about/versions/nougat/android-7.0-changes.html](https://developer.android.com/about/versions/nougat/android-7.0-changes.html).

## CWE/OWASP

 * OWASP Mobile Top 10: [M1 - Improper Platform Usage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M1-Improper_Platform_Usage)
 * CWE: [CWE-280 - Improper Handling of Insufficient Permissions or Privileges](http://cwe.mitre.org/data/definitions/280.html)
