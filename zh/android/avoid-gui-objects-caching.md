# Avoid GUI Objects Caching

Remote check-deposit apps allow people to take a picture of a check with their device and send it to their financial institution for deposit into an account.

## Details 

Android retains application screens in memory, and multitasking can result in the retention of an entire application in memory (even if the user logs out of their account). This allows an attacker that finds or steals a device to navigate directly to retained screens, which may include sensitive user data as part of the GUI. For example, if a user logs-out of a banking app but doesn't quit or close the app, a screen displaying transaction activity may be retained and viewable to an attacker.

## Remediation

To counter this, a developer has three common options:

1. Quit the app entirely when the user logs out. While it's against Android design principles to quit your own app, it's far more secure because quitting the app will destroy any retained GUI screens.

2. Any time an activity is initiated or a screen is accessed, execute a check to determine whether the user is in a logged-in state. If the user is not logged in, present the log-in screen.

3. Nullify the data on a GUI screen before leaving the screen or logging out.

## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200: Information Exposure](http://cwe.mitre.org/data/definitions/200.html)
