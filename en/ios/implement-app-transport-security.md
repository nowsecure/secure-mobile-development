# Implement App Transport Security (ATS)

## Details 

New in iOS 9, App Transport Security (ATS) helps ensure secure connections between an app and any back-end server(s). It is enabled by default when an app is linked against the iOS 9.0 SDK or later. With ATS enabled, HTTP connections are forced to use HTTPS (TLS v1.2) and any attempts to connect using insecure HTTP will fail.

Implementing ATS includes a couple of options:

* A developer can *enable* ATS globally (by linking to iOS 9.0 or later SDK) and then choose to decrease ATS restrictions on a specific server using an exception key
* A developer can *disable* ATS globally (by setting the NSAllowsArbitraryLoads key to YES) and then use an exception to increase ATS restrictions on a specific server

## Remediation

For apps running on iOS 9.0 or higher, best practice is to enable ATS globally by linking to the iOS 9.0 or later SDK and *NOT* setting the `NSAllowsArbitraryLoads` key to `Yes` or `True`.  Apple currently allows developers to include exceptions for any domains for which TLS cannot be enforced. Exceptions can be made using the `NSExceptionAllowsInsecureHTTPLoads` or `NSThirdPartyExceptionAllowsInsecureHTTPLoads` keys. It is important to note that beginning in January 2017, Apple will require appropriate justification from developers for any exceptions declared inside the application (during App Store review). Otherwise, all communications must use ATS.

## References

 * [App Transport Security REQUIRED January 2017](https://forums.developer.apple.com/thread/48979) - https://forums.developer.apple.com/thread/48979
 
## CWE/OWASP 

 * OWASP Mobile Top 10: [M3 - Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * CWE: [CWE-319 - Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
 
