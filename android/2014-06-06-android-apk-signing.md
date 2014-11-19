---
layout: guide
title: "Sign Android APKs"
description: "APKs should be signed correctly with a non-expired certificate."
published: 1
categories:
  - android	
series:
  name: Android
  index: 12
order: 612
--- 

## Details 

APKs should be signed correctly with a non-expired certificate.

## Remediation

A production app must be signed with a production certificate, not a debug certificate and the certificate must have sufficient time to expiry. Google recommend at least 2048 bit. The keystore containing the release signing key must be protected and held securely with the least number of people having access to it.

Here's an example of a Keytool command that generates a private key:

	$ keytool -genkey -v -keystore my-release-key.keystore
	
	-alias alias_name -keyalg RSA -keysize 2048 -validity 10000


## References

 * [https://developer.android.com/tools/publishing/app-signing.html#cert](https://developer.android.com/tools/publishing/app-signing.html#cert)

## CWE/OWASP

 * [M6 - Broken Cryptography](https://www.owasp.org/index.php/Mobile_Top_10_2014-M6)
 * [CWE 310](http://cwe.mitre.org/data/definitions/310.html), [326](http://cwe.mitre.org/data/definitions/326.html)
 
 