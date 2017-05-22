# Implement App Transport Security (ATS)

## Details

New in iOS 9, App Transport Security (ATS) helps ensure secure connections between an app and any back-end server(s). It is enabled by default when an app is linked against the iOS 9.0 SDK or later. With ATS enabled, HTTP connections are forced to use HTTPS (TLS v1.2) and any attempts to connect using insecure HTTP will fail.

Implementing ATS includes a couple of options:

* A developer can *enable* ATS globally (by linking to iOS 9.0 or later SDK) and then choose to decrease ATS restrictions on a specific server using an exception key
* A developer can *disable* ATS globally (by setting the NSAllowsArbitraryLoads key to YES) and then use an exception to increase ATS restrictions on a specific server

## Remediation

For apps running on iOS 9.0 or higher, best practice is to enable ATS globally by linking to the iOS 9.0 or later SDK and *NOT* setting the `NSAllowsArbitraryLoads` key to `Yes` or `True`.  Apple currently allows developers to include exceptions for any domains for which TLS cannot be enforced. Exceptions can be made using the `NSExceptionAllowsInsecureHTTPLoads` or `NSThirdPartyExceptionAllowsInsecureHTTPLoads` keys. Apple originally planned to require that all apps submitted to the App Store support ATS in January 2017, however, they have [extended the deadline](https://developer.apple.com/news/?id=12212016b) but have not yet announced a date.

Apple introduced the subkeys `NSAllowsArbitraryLoadsInWebContent`, `NSAllowsLocalNetworking`, and more in iOS 10. Developers can use these subkeys to disable only certain restrictions rather than overriding all ATS restrictions. For more information, see Apple documentation about [NSAppTransportSecurity and ATS configuration basics](https://developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW33) on the Apple Developer website.

## References

 * [Getting Ready for ATS Enforcement in 2017](https://nabla-c0d3.github.io/blog/2016/08/14/ats-enforced-2017/)
 * [Android buckles down and iOS opens up? Trends in platform security affecting developers](https://www.nowsecure.com/blog/2016/08/24/android-buckles-ios-opens-trends-platform-security-affecting-developers/)
 * [iOS 10 Security Changes Slide Deck](https://nabla-c0d3.github.io/blog/2016/09/19/ios10-slide-deck/)
 * [As of December, 2016, only 20 percent of apps enable ATS](https://www.nowsecure.com/blog/2016/12/29/enable-ios-app-transport-security-ats/)

## CWE/OWASP

 * OWASP Mobile Top 10: [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M3-Insecure_Communication)
 * CWE: [CWE-319 - Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
