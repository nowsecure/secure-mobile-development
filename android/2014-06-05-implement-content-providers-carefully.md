---
layout: guide
title: "Implement Content Providers Carefully"
description: "Content Providers are a standard way for apps to share data using a URI addressing scheme and relational DB model."
published: 1
categories:
  - android
series:
  name: Android
  index: 5
order: 608
--- 

## Details 

Content Providers are a standard way for apps to share data using a URI addressing scheme and relational DB model. They can also be used as a means to access “files” via the URI scheme.

## Remediation

Content Providers can declare permissions and can separate read and write access. Do not enable write access if not needed. Enable permissions to prevent any unprivileged app from reading the ContentProvider unless required.

Content Providers also allow record level delegation in order to share a specific record (or “file”) without sharing the entire database. Use this feature to provide the minimum access required for an operation. For example, you could share a single “Instant Message” with an external application which emails it to a contact without the external app having access to all messages. When the external app returns to the originating app, the delegation ends.

Parameters passed to content providers should be treated as untrusted input and not used directly in SQL queries without sanitization. SQL code can be sent in Content Provider requests and if included in a query can return data or control to an attacker.

Content providers that serve files based on a file name being passed to the provider should ensure path traversals are filtered out. For example, if an attacker includes "../../../file" it may cause the program to read files the attacker otherwise wouldn't have access to in the context of the application, and return this data to the attacker. Additionally be aware that following symlinks created by an attacker can have similar results.

## CWE/OWASP

 * [M7 - Client Side Injection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M7)
 * [CWE 926](http://cwe.mitre.org/data/definitions/316.html)
