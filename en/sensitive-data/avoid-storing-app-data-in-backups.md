# Avoid Storing App Data in Backups

## Details

Performing a backup of the data on an Android or iOS device can potentially also back-up sensitive information stored within an app’s private directory.

## Remediation

### Android

By default, the `allowBackup` flag within an Android app’s Manifest file is set as `true`. This results in an Android backup file (backup.ab) including all of subdirectories and files contained within an app’s private directory on the device’s file system. Therefore, explicitly declare the `allowBackup` flag as `false`.

### iOS

In performing an iTunes backup of a device on which a particular app has been installed, the backup will include all subdirectories (except the “Caches” subdirectory) and files contained within that app’s private directory on the device’s file system. Therefore, avoid storing any sensitive data in plaintext within any of the files or folders within the app’s private directory or subdirectories (see also best practice 3.1 [Implement Secure Data Storage](implement-secure-data-storage.md).

## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * CWE: [CWE-538 - File and Directory Information Exposure](http://cwe.mitre.org/data/definitions/538.html)
