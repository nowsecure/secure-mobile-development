---
layout: guide
title: "Be Aware of Copy and Paste"
description: "Both iOS and Android support copy/paste. Sensitive data may be stored, recoverable, or could be modified from the clipboard in clear text, regardless of whether the source of the data was initially encrypted."
published: 1
categories:
  - caching-and-logging
series:
  name: Caching and Logging
  index: 14
order: 306
--- 

## Details 

Both iOS and Android support copy/paste. Sensitive data may be stored, recoverable, or could be modified from the clipboard in clear text, regardless of whether the source of the data was initially encrypted. If it is in plaintext at the moment the user copies it, it will be in plaintext when other applications access the clipboard.

For example, it follows strictier rules, this means that applications cannot read or write the clipboard, and the only way to use it is by user interaction, doing long-taps to raise the clipboard menu.

## Remediation

Where appropriate, disable copy/paste for areas handling sensitive data. Eliminating the option to copy can help avoid data exposure. On Android the clipboard can be accessed by any application and so it is recommended that appropriately configured Content Providers be used to transfer complex sensitive data. On iOS consider whether the user will need to copy/paste data within the app or system-wide, and choose the appropriate type of pasteboard.

In addition, it can be interesting to clear the clipboard after taking the contents, to avoid other apps read them and leak what the user is doing.

## CWE/OWASP 

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
 
