---
layout: guide
title: "Use the Keychain carefully"
description: "iOS provides the Keychain for secure data storage. However, in several scenarios, the Keychain can be compromised and subsequently decrypted."
published: 1
categories:
  - ios
series:
  name: iOS
  index: 30
order: 501
--- 

## Details 

iOS provides the Keychain for secure data storage. However, in several scenarios, the Keychain can be compromised and subsequently decrypted.

In all versions of iOS up to and including iOS 7, Keychain can be partially compromised if attacker has access to the encrypted iTunes backup. Due to the way iOS re-encrypts Keychain entries when creating iTunes backups, it is possible to partially decrypt Keychain when iTunes backup is available and password for backup encryption is known (note that iTunes backups that are not encrypted do not allow decryption of Keychain items).

Keychain access controls are rendered ineffective if a “jailbreak” has been applied to the device. In this case any application running on the device can potentially read every other application’s Keychain items.

Lastly, for older devices, such as the iPhone 4, for which so-called “bootrom exploits” exist, the Keychain can be compromised by an attacker with physical access to the device.

## Remediation

When storing data in the Keychain, use the most restrictive protection class (as defined by kSecAttrAccessible attribute) that still allows your application to function properly. For example, if your application is not designed to be running in the background, use kSecAttrAccessibleWhenUnlocked or kSecAttrAccessibleWhenUnlockedThisDeviceOnly.

To prevent Keychain item exposure via iTunes backup, use one of ...ThisDeviceOnly protection classes if practical.

Finally, for highly sensitive data, consider augmenting protections offered by the Keychain with application-level encryption. For example, rely upon the user to enter a passphrase to authenticate within the application and use that passphrase to encrypt data before storing it into the Keychain.

## References
 
 * [Keychain Services Programming Guide][1]
	
## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2); [M5 - Poor Authorization and Authentication](https://www.owasp.org/index.php/Mobile_Top_10_2014-M5)
 * [CWE 312](http://cwe.mitre.org/data/definitions/312.html), [522](http://cwe.mitre.org/data/definitions/522.html)

<!-- Links -->
[1]: https://developer.apple.com/library/ios/documentation/security/Conceptual/keychainServConcepts/01introduction/introduction.html#//apple_ref/doc/uid/TP30000897
