# Limit Use of UUID
## Details

Most mobile devices have a unique ID, also called a Universal Unique Identifier (UUID), assigned at the time of manufacture for identification purposes. For example, iOS devices are assigned what's called a Unique Device Identifier (UDID). The ability to uniquely identify a device is often important to procure, manage and secure data. Developers quickly adopted the UUID and UDID for device identification, which resulted in it becoming a foundation of security for many systems.

Unfortunately, this approach brings with it several privacy and security issues. First, many online systems have connected the UUID of a device to an individual user to enable tracking across applications even when the user is not logged in to the app. This advanced ability to track a user has become a major privacy concern.

Beyond that, apps which identify a person through the UUID risk exposing the data of a device's previous owner to a new owner. In one instance, after re-setting an iPhone, we gained access to the prior user's account for an online music service even though all user data had been erased. Not only is this a privacy issue, it's a security threat because an attacker could fake a UUID.

Apple has recognized both the privacy and security risks of iOS's UDID and removed developer access to it. With the UDID out of reach, some developers apply other device-identification methods involving the MAC address of the wireless network interface or OpenUDID. These methods have now been banned at the system/API level and are also flagged and rejected as part of the AppStore review process.

## Remediation

We recommend that developers avoid using any device-provided identifier to identify the device, especially if it's integral to an implementation of device authentication. Instead, we recommend the creation of an app-unique "device factor" at the time of registration, installation, or first execution. This app-unique device factor in combination with user authentication can then be required to create a session. The device factor could also be used as an additional factor in an encryption routine.

Since it is not relying on predictable, device-supplied data, exploitation becomes more difficult. By leveraging a challenge-response approach, the server and device can authenticate each other prior to user authentication. To gain system access an attacker would have to exploit both factors. Developers can also implement a feature where the device factor is reset on the client or server side, forcing a more stringent re-authentication of the user and device.

To protect user privacy while preserving advertising capabilities, Apple recommends using the advertisingIdentifier - a unique identifier shared across all apps in the system. A person can reset the advertisingIdentifier on their device at any time in the Settings -> Privacy -> Advertising menu.

## References

 * [Unique Identifiers in iOS](https://possiblemobile.com/2013/04/unique-identifiers/)

## CWE/OWASP

 * [M7 - Client Code Quality](https://www.owasp.org/index.php/Mobile_Top_10_2016-M7-Poor_Code_Quality)
 * [CWE-200: Information Exposure](http://cwe.mitre.org/data/definitions/200.html)
