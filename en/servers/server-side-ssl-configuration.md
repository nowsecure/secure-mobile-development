# Properly Configure Server-side SSL

## Details

Many web servers allow lower encryption settings, such as the very weak, export-grade 40-bit encryption. Implement a strong cipher suite to protect information used in creating shared keys, encrypting messages between clients and servers, and generating message hashes and signatures that ensure the integrity of those messages. Also be sure to disable weak protocols.

## Remediation

Ensure SSL certificates are properly installed and configured for the highest encryption possible. If possible, enable only strong ciphers (128-bit and up).

TLSv1 is more than 10 years old and was found vulnerable to a “renegotiation attack” in 2009.

* Most servers using TLSv1 have been patched to close this vulnerability, but you should verify this for relevant servers.
* The TLSv1 protocol has been updated and the more current TLSv1.2 offers the latest technology and strongest encryption ciphers available. Updating to the newer version of TLS should harden and future-proof the application.

Avoid weak ciphers, such as:

* NULL cipher suite
* Anonymous Diffie-Hellmann
* DES and RC4 (because of their vulnerability to crypto-analytical attacks)

Avoid weak protocols, such as:

* SSLv2
* SSLv3 (because of its vulnerability to the POODLE attack - [CVE-2014-3566](https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2014-3566))
* TLS 1.0 and below (because the protocols are vulnerable to the CRIME and BEAST attacks - [CVE-2012-4929](http://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2012-4929) and [CVE-2011-3389](https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2011-3389) respectively)

Reference the OWASP [Transport Layer Protection Cheat Sheet](https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet) for more information about how to securely design and configure transport layer security for an app.

## References

* [Why Android SSL was downgraded from AES256-SHA to RC4-MD5 in late 2010](http://op-co.de/blog/posts/android_ssl_downgrade/) - http://op-co.de/blog/posts/android_ssl_downgrade/

## CWE/OWASP

 * [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * CWE: [CWE-326 - Inadequate Encryption Strength](http://cwe.mitre.org/data/definitions/326.html)
