# Institute Local Session Timeout

## Details 

Mobile devices are frequently lost or stolen, and an attacker can take advantage of an active session to access sensitive data, execute transactions, or perform reconnaissance on a device owner’s accounts. In addition, without a proper session timeout, an app may be susceptible to data interception via a man-in-the-middle attack.

## Remediation

Any time the app is not used for more than 5 minutes, terminate the active session, redirect the user to the log-in screen, ensure that no app data is visible, and require the user to re-enter log-in credentials to access the app.

After timeout, also discard and clear all memory associated with user data including any master keys use to decrypt that date (see also best practice 2.5 [Securely Store Sensitive Data in RAM](/coding-practices/securely-store-sensitive-data-in-ram.md))

Also, make sure the session timeout occurs on both the client side and the server side to mitigate against an attacker modifying the local timeout mechanism. 

## CWE/OWASP 

 * OWASP Mobile Top 10: [M9 - Improper Session Handling](https://www.owasp.org/index.php/Mobile_Top_10_2014-M9)
 * CWE: [CWE-613 - Insufficient Session Expiration](http://cwe.mitre.org/data/definitions/613.html)
 
