# Use SECURE Setting For Cookies

## Details 

If a cookie is not marked as secure, it may be transmitted over insecure connection whether or not the session with the host is secure. In other words, it may be be transmitted over an HTTP connection.

## Remediation

The Set-Cookie headers should use the SECURE setting. This setting should be applied to all cookies for native or web apps leveraging HTTPS.

## CWE/OWASP 

 * [M9 - Improper Session Handling](https://www.owasp.org/index.php/Mobile_Top_10_2014-M9)
 * [CWE 614](http://cwe.mitre.org/data/definitions/79.html)
 
