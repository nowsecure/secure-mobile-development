# Protect Against SSL Downgrade Attacks

## Details

Using this form of a man-in-the-middle attack, an attacker can bypass SSL/TLS by transparently hijacking HTTP traffic on a network, monitoring for HTTPS requests, and then eliminating SSL/TLS, which creates an unsecured connection between the client and server. This attack can be particularly difficult to prevent on mobile web apps (mobile web apps are essentially webpages made to look like an app).

## Remediation

Serve all traffic, even non-sensitive traffic,over TLS. This prevents any possible downgrading/stripping attacks because an attacker needs an initial plaintext “entry point” to accomplish said attack.

Validate that SSL/TLS is active. Validating SSL/TLS is relatively straight-forward in fully native apps. Mobile web apps can validate SSL/TLS through JavaScript so that if an HTTPS connection is not detected, the client redirects to HTTPS. A more reliable means to require SSL/TLS is the HTTP Strict Transport Security (HSTS) header. The HSTS header forces all subsequent connections to that domain to use TLS and the original certificate. Browsers are only starting to implement the HSTS header and mobile browser support lags behind. 

Avoid using icons or language  within the app that assures users of a secure connection when said connection does not depend on a validated HTTPS session. User education is an important component in reducing the risk of SSL/TLS downgrade attacks. Use alerts and text within the app to reinforce to users the importance of protecting network traffic using HTTPS.

Another mitigation recently put in place within both Android and iOS is to treat non-TLS/plaintext traffic as a developer error. Android recently added `android:usesCleartextTraffic` ([Android M and the War on Cleartext Traffic](https://koz.io/android-m-and-the-war-on-cleartext-traffic/) - https://koz.io/android-m-and-the-war-on-cleartext-traffic/), and iOS 9 and above require that you manually add exceptions for plaintext traffic. Replacement web protocol HTTP/2 is another future mitigation because it uses only TLS (and includes other features).

## References

* [Moxie Marlinspike’s sslstrip exploitation tool](https://moxie.org/software/sslstrip/) - https://moxie.org/software/sslstrip/

## CWE/OWASP

 * OWASP Mobile Top 10: [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * CWE: [CWE-757: Selection of Less-Secure Algorithm During Negotiation ('Algorithm Downgrade')](http://cwe.mitre.org/data/definitions/757.html)


