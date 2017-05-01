# Implement File Permissions Carefully

## Details

World readable files can act as a vector for your program to leak sensitive information. World writeable files may expose your app by letting an attacker influence its behavior by overwriting data that is read by your app from storage.  Examples include settings files and stored login information.

## Remediation

Do not create files with permissions of MODE_WORLD_READABLE or MODE_WORLD_WRITABLE unless it is required as any app would be able to read or write the file even though it may be stored in the app’s private data directory.

_Note: these constants were deprecated in Android API level 17. Source: [http://developer.android.com/reference/android/content/Context.html](http://developer.android.com/reference/android/content/Context.html)_

Do not use modes such as 0666, 0777, and 0664 with the chmod binary or syscalls accepting a file mode (chmod, fchmod, creat, etc)

## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * [CWE 280](http://cwe.mitre.org/data/definitions/280.html)
