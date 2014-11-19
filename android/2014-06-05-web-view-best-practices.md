---
layout: guide
title: "Follow WebView Best Practices"
description: "WebViews can introduce a number of security concerns and should be implemented carefully."
published: 1
categories:
  - android
series:
  name: Android
  index: 11
order: 609
--- 

## Details 

WebViews can introduce a number of security concerns and should be implemented carefully. In particular, many vulnerabilities have been discovered that exploit the use of the addJavscriptInterface API.

## Remediation

Disable JavaScript and Plugin support if they are not needed. They are disabled by default but it is good practice to explicitly set these.  Disable local file access. This restricts access to the app’s resource and asset directory and mitigates against an attack from a web page which seeks to gain access to other locally accessible files.

Prevent loading content from 3rd party hosts. This is tricky to completely prevent from within an app but a developer can override shouldOverrideUrlLoading and shouldInterceptRequest to intercept, inspect, and validate most requests initiated from within a WebView.  A whitelist scheme can also be implemented by using the URI class to inspect the components of a URI and ensure it matches a whitelist of approved resources.

Sample code [https://gist.github.com/scottyab/6f51bbd82a0ffb08ac7a](https://gist.github.com/scottyab/6f51bbd82a0ffb08ac7a)

## References 

 * [http://labs.mwrinfosecurity.com/blog/2012/04/23/adventures-with-android-webviews/](http://labs.mwrinfosecurity.com/blog/2012/04/23/adventures-with-android-webviews/)
 * [https://developer.android.com/training/articles/security-tips.html#WebView](https://developer.android.com/training/articles/security-tips.html#WebView)
 
## CWE/OWASP

 * [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 79](http://cwe.mitre.org/data/definitions/79.html)