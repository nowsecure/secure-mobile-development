# Protect and Pen Test Web Services

## Details

A compromised server has the potential to intercept user credentials and launch other attacks against app users.

## Remediation

In general, a production web server must be thoroughly tested and hardened against malicious attack.   Production server software should be updated to the latest versions, and hardened to prevent information disclosures regarding server software and interfaces.

Authentication forms should not reflect whether a username exists. If an attacker has a method to determine valid usernames, they have a starting point for brute-force and phishing attacks. Prevent username harvesting by providing the same response back to the client for both “invalid user/pass combination” and “no such username found” events.  All login forms and forms/pages exchanging sensitive data should implement and require HTTPS. Web servers should not allow client connections without SSL for such resources. Turn off verbose errors, remove any legacy unnecessary sites or pages, and continually harden Web resources against potential attacks.

## References


## CWE/OWASP

 * [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * [CWE 307](http://cwe.mitre.org/data/definitions/307.html), [200](http://cwe.mitre.org/data/definitions/200.html), etc. (could be multiple)
