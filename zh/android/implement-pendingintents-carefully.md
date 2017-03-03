# Implement PendingIntents Carefully

A PendingIntent allows an app to pass an Intent to a second application that can then execute that Intent as if it were the originating app (i.e., with the same permissions).

## Details 

With a PendingIntent, an app can pass an Intent to a second application that can then execute that Intent as if it were the originating app (i.e., with the same permissions). This allows other apps to call back to the originating app's private components.  The external app, if malicious, may try to influence the destination and/or data/integrity.

## Remediation

Use PendingIntents as delayed callbacks to private BroadcastReceivers or broadcast activities, and explicitly specify the component name in the base Intent.

## References 

 * Sample code here [https://gist.github.com/scottyab/d5ab6a284622ebc46d5a](https://gist.github.com/scottyab/d5ab6a284622ebc46d5a)

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE-927: Use of Implicit Intent for Sensitive Communication](http://cwe.mitre.org/data/definitions/927.html)
