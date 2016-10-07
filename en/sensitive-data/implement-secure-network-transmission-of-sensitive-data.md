# Implement Secure Network Transmission Of Sensitive Data

## Details 

Unlike web browsers, mobile devices typically do not disclose whether or not an app uses SSL/TLS to secure the transmission of data, and so app users simply have to trust that the app’s developer has implemented network encryption.

For many years SSL (followed by TLS) has been the standard for encryption of web communications, including the web services that power mobile apps. However breaches of certifying authorities like DigiNotar and Comodo exposed many users to bogus certificates. The Apple “[goto fail](https://avandeursen.com/2014/02/22/gotofail-security/)” bug further exposed the limits of SSL/TLS’s reliability for app developers.

Today, best practices call for app providers to use SSL/TLS effectively to secure the transmission of passwords, login IDs, and other sensitive data over the network, and even go further and leverage app-layer encryption to protect user data.

## Remediation

Use SSL/TLS either with standard trust validation, or, for increased security, implement  certificate pinning (see also best practice 3.3 [Fully Validate SSL/TLS](fully-validate-ssl-tls.md) and the OWASP “[Pinning Cheat Sheet](https://www.owasp.org/index.php/Pinning_Cheat_Sheet)”).

To prevent the interception of highly sensitive values (e.g., login IDs, passwords, PINs, account numbers, etc.) via a compromised SSL/TLS connection, implement additional encryption in transit. Encrypt highly sensitive values with AES (also known as Rijndael) using a key size of 256. For hashing purposes, use an algorithm such as SHA-256 or higher.

On the server side, consider accepting only strong TLS ciphers and keys and disabling lower levels of encryption such as export-grade 40-bit encryption (see also best practice 8.2 [Properly Configure Server-Side SSL](../servers/server-side-ssl-configuration)) 

## CWE/OWASP 

 * OWASP Mobile Top 10: [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * CWE: [CWE-311 - Missing Encryption of Sensitive Data](http://cwe.mitre.org/data/definitions/311.html), [CWE-319 - Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
