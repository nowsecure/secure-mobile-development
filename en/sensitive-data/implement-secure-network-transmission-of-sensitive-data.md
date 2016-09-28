# Implement Secure Network Transmission Of Sensitive Data

## Details 

In most cases, app users simply have to trust that developers implement network encryption because unlike web browsers, mobile devices do not display whether or not an app is using SSL/TLS.

For many years SSL (followed by TLS) has been the standard for encryption of web communications, including the web services that power mobile apps. But is it still enough? In recent years, breaches of certifying authorities like Diginotar and Comodo exposed many users to bogus certificates. The Apple “goto fail” bug further exposed the limits of SSL/TLS reliability for app developers.

Today, best practices call for app providers to use SSL/TLS effectively to secure passwords and private data on the network, and even go further and leverage app-layer encryption to protect their users.

## Remediation

Use SSL/TLS either with standard trust validation, or leverage certificate pinning for higher security.

To secure passwords and sensitive data on the network and protect against SSL/TLS-related flaws and attacks, apps can use asymmetric or symmetric encryption with varying degrees of complexity and security.


## CWE/OWASP 

 * [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * [CWE-319: Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
 * [CWE-311: Missing Encryption of Sensitive Data](http://cwe.mitre.org/data/definitions/311.html)
