# Use Proper Session Management

## Details

Sessions for users are maintained on most apps via a cookie, which can be vulnerable.


## Remediation

Web languages (e.g. Java, .NET) offer session management, which is well-developed and security tested. Keep server software up-to-date with security patches. Rolling your own session management is more risky and undertaken only with proper expertise.  Ensure the size of the session cookie is sufficient. Short or predictable session cookies make it possible for an attacker to predict, highjack or perform other attacks against the session. Use high-security settings in session configuration.


## CWE/OWASP

 * [M6 - Insecure Authorization](https://www.owasp.org/index.php/Mobile_Top_10_2016-M6-Insecure_Authorization)
 * [CWE 613](http://cwe.mitre.org/data/definitions/613.html)
