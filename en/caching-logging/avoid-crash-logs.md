# Avoid Crash Logs

## Details

There are several frameworks for tracking user usage and collect crash logs for iOS and Android, both are useful tools for development, but it is important to find a balance between enough debug information for the developers and reduced information for attackers.

If an app crashes, the resulting log can provide valuable info to an attacker.

## Remediation

Ensure released apps are built without warnings and are thoroughly tested to avoid crashes. This is certainly always the goal and worth mentioning due to the value of a crash log. Consider disabling NSAssert for iOS. This setting will cause an app to crash immediately if an assertion fails. It is more graceful to handle the failed assertion than to crash and generate the crash log. Also, avoid sending crash logs over the network in plaintext.

Use secure development tools like clang-analyzer, coverity, ASAN and other linting utilities in order to identify all possible operations that can make the app crash or missfunction.

In addition, if the app is obfuscated and stripped, the developer will need keep an address-to-symbol database in order to recover meaningful backtraces in crashlogs, making attacker's life harder because of the lack of understandable names in functions.

## CWE/OWASP

 * [M7 - Client Code Quality](https://www.owasp.org/index.php/Mobile_Top_10_2016-M7-Poor_Code_Quality)
 * [CWE 215](http://cwe.mitre.org/data/definitions/215.html)
