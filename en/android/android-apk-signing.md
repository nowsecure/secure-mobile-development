# Sign Android APKs

## Details

APKs should be signed correctly with a non-expired certificate.

## Remediation

- Sign a production app with a production certificate, not a debug certificate
- Make sure the certificate includes a sufficient validity period (i.e., won't expire during the expected lifespan of the app)
- Google recommends that your certificate use at least 2048-bit encryption
- Make sure the keystore containing the signing key is properly protected
- Also, restrict access to the keystore to only those people that absolutely require it

Here's an example of a Keytool command that generates a private key:

```
$ keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
```

## References

 * [https://developer.android.com/tools/publishing/app-signing.html#cert](https://developer.android.com/tools/publishing/app-signing.html#cert)

## CWE/OWASP

 * [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * [CWE-310: Cryptographic Issues](http://cwe.mitre.org/data/definitions/310.html)
 * [CWE-326: Inadequate Encryption Strength](http://cwe.mitre.org/data/definitions/326.html)
