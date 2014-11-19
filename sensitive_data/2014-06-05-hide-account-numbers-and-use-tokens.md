---
layout: guide
title: "Hide Account Numbers and Use Tokens"
description: "Many apps store complete account numbers in the various screens."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 8
order: 211
--- 

## Details 

Many apps store complete account numbers in various screens.

## Remediation

Given the widespread use of mobile apps in public places, displaying partial numbers (e.g. ***9881) can help ensure maximum privacy for this information. Unless there is a need to store the complete number on the device, store the partially hidden numbers.  Often, account numbers are used to reference server-side account data; this data can easily be stolen from memory, or in some cases manipulated to work with accounts that the user should not have permission to access. It is recommended that instead of account numbers, tokens be assigned to each account and provided to the client. These tokens, which should not be deducible by the user, have server-side mapping to an actual account. Should the application data be stolen, the user’s account numbers will not be exposed, and an attacker will also not be able to reference account numbers directly, but must first determine the token that maps back to the account.

In iOS, if you realize

```
> - (BOOL)textField:(UITextField *)textField 

> shouldChangeCharactersInRange:(NSRange)range replacementString:(NSString *)string
```

as part of the delegate for the text field, you can change the visibility of the entered text.