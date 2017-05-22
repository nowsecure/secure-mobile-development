# Implement Touch ID Properly

## Details

Touch ID is commonly known for its use in allowing a user to authenticate to and unlock their device without entering a passcode. Some developers also use Touch ID to allow the user to authenticate to their app using a fingerprint previously registered with the device.

When a developer implements Touch ID in their app, they typically do so in one of two ways:

1. Using only the Local Authentication framework to authenticate the user.
    * This method leaves the authentication mechanism vulnerable to bypass.
    * An attacker can modify the local check at runtime, or by patching the binary. This is done by overriding the `LAContextevaluatePolicy:localizedReason:reply` method implementation.
2. Using Keychain access control lists (ACLs).

## Remediation

When using Touch ID for authentication, store the app’s secret in the Keychain with an ACL assigned to that item. With this method, iOS performs a user presence check before reading and returning Keychain items to the app. Developers can find sample code on the Apple website at [https://developer.apple.com/library/ios/samplecode/KeychainTouchID/Listings/KeychainTouchID_AAPLKeychainTestsViewController_m.html](https://developer.apple.com/library/ios/samplecode/KeychainTouchID/Listings/KeychainTouchID_AAPLKeychainTestsViewController_m.html).

NOTE - Note - Developers can use Touch ID enrollment changes to detect and prevent a physically proximate attacker from enrolling their own fingerprint in order to gain access to protected Keychain items. Beginning with iOS 9, an app can read `LAContext.evaluatedPolicyDomainState` to check whether the `evaluatedPolicyDomainState` value has changed. If the value has changed, it indicates that Touch ID enrollment changes have occurred since it was last accessed.

See “Keychain access control” under the Keychain Data Protection section of the [iOS Security Guide](https://www.apple.com/business/docs/iOS_Security_Guide.pdf) for more information.

## References

 * Apple documentation: [KeychainTouchID: Using Touch ID with Keychain and LocalAuthentication](https://developer.apple.com/library/content/samplecode/KeychainTouchID/Introduction/Intro.html) - https://developer.apple.com/library/content/samplecode/KeychainTouchID/Introduction/Intro.html

## CWE/OWASP

 * OWASP Mobile Top 10: [M4 - Insecure Authentication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M4-Insecure_Authentication), [M6 - Insecure Authorization](https://www.owasp.org/index.php/Mobile_Top_10_2016-M6-Insecure_Authorization)
 * CWE: [CWE-288 - Authentication Bypass Using an Alternate Path or Channel](http://cwe.mitre.org/data/definitions/288.html)
