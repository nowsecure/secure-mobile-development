# Protect Application Settings

## Details

iOS developers often store application settings in plist files which can be compromised in some situations. Similarly, Android developers often store settings in a shared preferences XML file or SQLite databases, which are not encrypted by default and can be read or even modified with root permissions, or using backup procedures.

## Remediation

Compile settings into the code when possible. There is little benefit to configuring an app via plist file on iOS since changes must be bundled and deployed as a new app anyway. Instead, include configuration inside app code which requires more time and skill for attackers to modify.  Don’t store any critical settings in dictionaries or other files unless encrypted first. Ideally, encrypt all configuration files using a master key encrypted with a passphrase that is supplied by the user, or with a key provided remotely when a user logs into a system.

## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * [CWE 312](http://cwe.mitre.org/data/definitions/312.html), [313](http://cwe.mitre.org/data/definitions/313.html)
