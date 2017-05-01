# Protect Internal Resources

## Details

Resources for internal use such as administrator login forms frequently leverage authentication that is not resistant to brute force. For example HTTP or forms authentication without lockout. Compromise of administration or other internal resources can lead to extensive data loss and other damage.

## Remediation

Such resources should be blocked from external access.   Any resource that does not require public Internet access should be restricted using firewall rules and network segmentation. If a login page, admin area or other resource is accessible externally, assume it will be discovered by malicious users and attacked by brute force.

## CWE/OWASP

 * [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * [CWE 200 - Multiple CWE's](http://cwe.mitre.org/data/definitions/200.html)
