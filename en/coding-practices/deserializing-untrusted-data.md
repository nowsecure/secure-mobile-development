# 2.8 Use caution in deserializing untrusted data

## Details

Developers typically serialize (or “marshal”) data to transfer application state between systems or store it for later use. Deserializing (or “unmarshalling”) that serialized data will then reconstruct the data, or in some cases reconstruct application logic. Unfortunately, an application might assume that the deserialized data is valid or trusted, a situation that an attacker can exploit to modify the regular execution flow of the app.  This security flaw applies to both iOS and Android apps (particularly Binder operations in Android).

## Remediation

Generally, you can prevent vulnerabilities arising from the deserialization of untrusted data in four ways:
1. Identify trust boundaries between systems, treating data attributed from external sources as untrusted
2. Avoid the deserialization of data from untrusted sources
3. Sanitize the deserialized data (e.g., only allow known safe characters, objects, limited functionality)
4. Validate and authenticate the provenance and contents of a file before deserializing it.

## REFERENCES

### General
* [OWASP - Deserialization of untrusted data](https://www.owasp.org/index.php/Deserialization_of_untrusted_data)
* [OWASP Deserialization Cheat Sheet](https://www.owasp.org/index.php/Deserialization_Cheat_Sheet)

### iOS
* [Everything you need to know about NSSecureCoding](http://nshipster.com/nssecurecoding/)
* [The Java Deserialization Bug and NSSecureCoding](https://mjtsai.com/blog/2015/11/08/the-java-deserialization-bug-and-nssecurecoding/)

### Android
* [CVE-2014-7911 – A Deep Dive Analysis of Android System Service Vulnerability and Exploitation](http://researchcenter.paloaltonetworks.com/2015/01/cve-2014-7911-deep-dive-analysis-android-system-service-vulnerability-exploitation/)


## CWE/OWASP

* OWASP Mobile Top 10: [M7 - Client Code Quality](https://www.owasp.org/index.php/Mobile_Top_10_2016-M7-Poor_Code_Quality)
* CWE: [CWE-502: Deserialization of Untrusted Data](http://cwe.mitre.org/data/definitions/502.html)
