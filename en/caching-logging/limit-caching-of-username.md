# Limit Caching of Username

## Details

On iOS, when the user enables the “Save this User ID” feature, the username is cached within the CredentialsManager object. At runtime, the username is loaded into memory before any type of authentication occurs, allowing potential for a malicious process to intercept the username.

## Remediation

It is difficult to offer the user convenience of a stored username while avoiding leakage of such information either through insecure storage or potential interception at runtime. Although not as sensitive as the password, username is private data that should be protected. One potential method that offers a cached username option with higher security is to store a masked username instead of the actual username, and replace the username value in authentication with a hash value. The hash value can be created including a unique device token stored on registration. The benefit of a process that uses a hash and device token is that the actual username is not stored locally or loaded into memory unprotected, and the value copied to another device or used on web would not be adequate. A malicious user would have to uncover more information to successfully steal the authentication username.


## References

 * [http://resources.infosecinstitute.com/ios-application-security-part-20-local-data-storage-nsuserdefaults-coredata-sqlite-plist-files/](http://resources.infosecinstitute.com/ios-application-security-part-20-local-data-storage-nsuserdefaults-coredata-sqlite-plist-files/)

## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage), [M7 - Client Code Quality](https://www.owasp.org/index.php/Mobile_Top_10_2016-M7-Poor_Code_Quality)
 * [CWE 312](http://cwe.mitre.org/data/definitions/312.html), [313](http://cwe.mitre.org/data/definitions/313.html), [522](http://cwe.mitre.org/data/definitions/522.html)
