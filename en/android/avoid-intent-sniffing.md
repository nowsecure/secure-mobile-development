# Avoid Intent Sniffing

When an activity is initiated by another application using a broadcast intent, the data passed in the intent can be read by a malicious app.

## Details

When another application initiates activity by sending a broadcast intent, malicious apps can read the data included in the intent. The malicious app can also read a list of recent intents for an application. For example, if an app invokes and passes a URL to the Android web browser, an attacker could sniff that URL.

## Remediation

Do not pass sensitive data between apps using broadcast intents. Instead, use explicit intents.

## CWE/OWASP

 * [M7 - Client Code Quality](https://www.owasp.org/index.php/Mobile_Top_10_2016-M7-Poor_Code_Quality), [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * [CWE 285: Improper Authorization](http://cwe.mitre.org/data/definitions/285.html)
