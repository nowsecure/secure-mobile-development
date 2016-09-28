---
layout: guide
title: "Implement Content Providers Carefully"
description: "Content providers are a standard way for apps to share data using a URI-addressing scheme and relational database model."
published: 1
categories:
  - android
series:
  name: Android
  index: 5
order: 608
--- 

## Details 

Content providers allow apps to share data using a URI-addressing scheme and relational database model. They can also be used to access files via the URI scheme.

## Remediation

Content providers can declare permissions and separate read and write access. Do not give a content provider write access unless it's absolutely necessary. Make sure to set permissions so that unprivileged apps cannot read the `ContentProvider` instance unless required.

Limit access to the minimum required for an operation. For example, to share an instant message with another app that emails that message to a contact, share only that single message and not all instant messages. The record-level delegation feature within content providers allows for the sharing of a specific record or file without sharing the entire database. Once the external app returns to the originating app, the delegation ends.

Treat parameters passed to content providers as untrusted input and don't use them directly in SQL queries without sanitation. Without sanitation, SQL code can be sent via content provider requests. If the SQL code is included in a query, it can return data or give control to an attacker.

Content providers that serve files based on a file name being passed to the provider should ensure path traversals are filtered out. For example, if an attacker were to include `../../../file` in a request, it could cause the program to read and return data from files the attacker wouldn't otherwise have access to in the context of the application. Additionally, be aware that following symlinks created by an attacker can have similar results.

## CWE/OWASP

 * [M7 - Client Side Injection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M7)
 * [CWE 926: Improper Export of Android Application Components](http://cwe.mitre.org/data/definitions/926.html)
