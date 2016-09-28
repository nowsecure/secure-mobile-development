# Properly Configure Server-side SSL

## Details 

Many web servers allow lower encryption settings, such as the very weak export-grade 40-bit encryption.

## Remediation

Ensure SSL certificates are properly installed and configured for the highest encryption possible. If possible, enable only strong ciphers (128-bit and up) and SSLv3/TLSv1.  TLSv1 is more than 10 years old and was found vulnerable to a “renegotiation attack” in 2009. Most servers using TLSv1 have been patched to close this vulnerability, but this should be verified. The TLSv1 protocol has been updated and the more current TLSv1.2 offers the latest technology and strongest encryption ciphers available. Updating to the newer version of TLS should harden and future-proof the application.
 
Code samples in a commit to Onionkit’s StrongSSLSocketFactory.java shows how to set the default Cipher suite and protocol version to prefer stronger encryption.

[https://github.com/guardianproject/NetCipher/blob/master/libnetcipher/src/info/guardianproject/onionkit/trust/StrongSSLSocketFactory.java](https://github.com/guardianproject/NetCipher/blob/master/libnetcipher/src/info/guardianproject/onionkit/trust/StrongSSLSocketFactory.java) 

## References 

[http://op-co.de/blog/posts/android_ssl_downgrade/](http://op-co.de/blog/posts/android_ssl_downgrade/)

## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 326](http://cwe.mitre.org/data/definitions/326.html)
