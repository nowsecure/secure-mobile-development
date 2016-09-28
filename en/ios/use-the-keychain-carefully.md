# Use the Keychain Carefully

## Details 

iOS provides the keychain for secure data storage. However, in several scenarios, the keychain can be compromised and subsequently decrypted.

In all versions of iOS up to and including iOS 7, the keychain can be partially compromised if an attacker has access to the encrypted iTunes backup. Because of how iOS re-encrypts keychain entries when creating iTunes backups, the keychain can be partially decrypted when an iTunes backup is available and the password for backup encryption is known. However, iTunes backups that are not encrypted do not allow for the decryption of keychain items.

Keychain access controls are rendered ineffective if a jailbreak has been applied to the device. In the case of a jailbreak, any application running on the device can potentially read every other application’s keychain items.

Lastly, for older devices (e.g., iPhone 4) for which BootROM exploits exist, the keychain can be compromised by an attacker that has physical access to the device.

## Remediation

When storing data in the keychain, use the most restrictive protection class (as defined by the `kSecAttrAccessible` attribute) that still allows your application to function properly. For example, if your application is not designed to run in the background, use `kSecAttrAccessibleWhenUnlocked` or `kSecAttrAccessibleWhenUnlockedThisDeviceOnly`.

To prevent the exposure of keychain items via iTunes backup, use the ThisDeviceOnly protection class where practical.

Finally, for highly sensitive data, consider augmenting protections offered by the keychain with application-level encryption. For example, rely upon the user to enter a passphrase to authenticate within the application, and then use that passphrase to encrypt data before storing it into the Keychain.

## References
 
 * [Keychain Services Programming Guide][1]
	
## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2); [M5 - Poor Authorization and Authentication](https://www.owasp.org/index.php/Mobile_Top_10_2014-M5)
 * [CWE-312: Cleartext Storage of Sensitive Information](http://cwe.mitre.org/data/definitions/312.html)
 * [CWE-522: Insufficiently Protected Credentials](http://cwe.mitre.org/data/definitions/522.html)

<!-- Links -->
[1]: https://developer.apple.com/library/ios/documentation/security/Conceptual/keychainServConcepts/01introduction/introduction.html#//apple_ref/doc/uid/TP30000897
