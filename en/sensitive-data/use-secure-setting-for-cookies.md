# Use SECURE Setting For Cookies

## Details

If a cookie is not marked as “Secure,” it may be transmitted over an insecure connection whether or not the session with the host is secure. In other words, it may be be transmitted over an HTTP connection.

In addition, setting the "HTTPOnly" flag on a cookie prevents attacks such as cross-site scripting (XSS), because the cookie cannot be accessed via the client side (e.g., cannot be accessed using a snippet of JavaScript code).

## Remediation

The Set-Cookie headers should use the “Secure” and “HTTPOnly” settings. These settings should be applied to all cookies for native and/or web apps.

## CWE/OWASP

 * [M6 - Insecure Authorization](https://www.owasp.org/index.php/Mobile_Top_10_2016-M6-Insecure_Authorization)
 * CWE [CWE-614 - Sensitive Cookie in HTTPS Session Without 'Secure' Attribute](http://cwe.mitre.org/data/definitions/79.html)
