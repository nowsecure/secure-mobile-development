---
title: "Avoid GUI Objects Caching"
description: "Remote check deposit apps allow the user to take a picture of a check using the phone’s camera and send it off to the financial institution to deposit in an account."
layout: guide
published: 1
categories:
 - android
section: Android
series:
  name: Android
  index: 1
order: 611
--- 

## Details 

On Android, application screens are retained in memory and entire applications can be retained in memory because of multitasking. An attacker who finds or steals a device is able to navigate directly to previously used screens that are still retained and see any data still shown on the GUI. An example of this would be a banking application where a user views their transaction history and then “logs out” of the application. By launching the transaction view activity directly the attacker can see the previous transactions that were displayed.

## Remediation

To counter this, a developer has three common options:

1. Quit the app entirely when the user logs out. It is against Android design principles to quit your own app but it is more secure as the GUI gets destroyed/recycled.

2. Perform a test at the start of each Activity/screen to check if the user is in a logged in state, if not, switch to the login screen.

3. Nullify the data on a GUI screen before leaving the screen or logging out.

## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
