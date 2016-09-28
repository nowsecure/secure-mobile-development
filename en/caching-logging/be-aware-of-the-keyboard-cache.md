# Be Aware of the Keyboard Cache

## Details 

iOS logs what users type in order to provide features such as customized auto-correct and form completion, but sensitive data may also be stored. Almost every non-numeric word is cached in the keyboard cache in the order it was typed; the cache’s contents are beyond the administrative privileges of the application, and so the data cannot be removed from the cache by the application.

## Remediation

Disable the auto-correct feature for any sensitive information, not just for password fields. Since the keyboard caches sensitive information, it may be recoverable. For UITextField, look into setting the autocorrectionType property to UITextAutocorrectionTypeNo to disable caching. These settings may change over time as the SDK updates so ensure it is fully researched. Add an enterprise policy to clear the keyboard dictionary at regular intervals. This can be done by the end user by simply going to the Settings application, General > Reset > Reset Keyboard Dictionary. 

Android contains a user dictionary, where words entered by a user can be saved for future auto-correction. This user dictionary is available to any app without special permissions.  For increased security, consider implementing a custom keyboard (and potentially PIN entry), which can disable caching and provide additional protection against malware.

## CWE/OWASP 

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
 
