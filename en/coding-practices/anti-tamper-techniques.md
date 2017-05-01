# Implement Anti-tamper Techniques

## Details

Attackers can tamper with or install a backdoor on an app, re-sign it and publish the malicious version to third-party app marketplaces. Such attacks typically target popular apps and financial apps.

## Remediation

Employ anti-tamper and tamper-detection techniques to prevent illegitimate applications from executing.

Use checksums, digital signatures and other validation mechanisms to help detect file tampering. When an attacker attempts to manipulate the application, the correct checksum would not be preserved and this could detect and prevent illegitimate execution. Note that such techniques are not foolproof and can be bypassed by a sufficiently motivated attacker. Checksum, digital signature and other validation techniques increase the amount of time and effort an attacker must spend to successfully breach the application. An application can silently wipe its user data, keys, or other important data wherever tampering is detected to further challenge an attacker. Applications that have detected tampering can also notify an administrator.

On Android, the public key used to sign an app can be read from the app’s certificate and used to verify the application was signed with the developer’s private key. Using the PackageManager class, it’s possible to retrieve the signatures of our application and then compare them with the correct value. If someone has tampered with or re-signed the application, the comparison will fail resulting in the detection of tampering with the application.

## References

 * Android - [https://gist.github.com/scottyab/b849701972d57cf9562e](https://gist.github.com/scottyab/b849701972d57cf9562e)

## CWE/OWASP

 * [M9 - Reverse Engineering](https://www.owasp.org/index.php/Mobile_Top_10_2016-M9-Reverse_Engineering), [M8 - Code Tampering](https://www.owasp.org/index.php/Mobile_Top_10_2016-M8-Code_Tampering)
 * [CWE-354: Improper Validation of Integrity Check Value](http://cwe.mitre.org/data/definitions/354.html)
