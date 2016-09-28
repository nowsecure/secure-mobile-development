---
layout: guide
title: "Prevent Framing and Clickjacking"
description: "Framing involves delivery of a Web/WAP site within an iFrame."
published: 1
categories:
  - webviews
series:
  name: Webviews
  index: 41
order: 401
--- 

## Details 

Framing involves delivery of a Web/WAP site within an iFrame. This attack can enable the “wrapper” site to execute a clickjacking attack. Clickjacking is a very real threat that has been exploited on high-profile services (e.g., Facebook) to steal information or redirect users to attacker controlled sites.
The primary purpose for framing is to trick users into clicking on something different that what they intended. The goal is to gather confidential information or take control of the affected computer through chained vulnerabilities like Cross Site Scripting. This attack commonly takes the form of a script that is embedded within the source code, which is executed without the user’s knowledge.  It can be triggered when users click a button that appears to perform other function.

## Remediation

The best way to prevent this practice in iOS is to not use WebViews. Also use

``` 
- (NSString *)stringByEvaluatingJavaScriptFromString:(NSString *)script
```

very, very carefully [(click here for more info on the NSString Class Reference)](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSString_Class/Reference/NSString.html#//apple_ref/doc/c_ref/NSString).

One mechanism for the prevention of framing leverages client-side JavaScript. Most Web sites are no longer designed or able to run without JavaScript, so the implementation of security measures in JavaScript (and disabling site without it) is an option. Though client-side and therefore not impervious to tampering, this layer does raise the bar for the attacker.  Below is an example of JavaScript code that forces the site to the “top” frame, thereby “busting” a frame which had loaded the site.

There are additional steps an attacker can add to their frame to attempt to prevent the frame busting code, such as an alert to the user on unload asking them not to exit. More complex JavaScript may be able to counter such techniques. The inclusion of at least basic frame busting code makes simple framing a much more difficult process.

**X-FRAME-OPTIONS HEADER**– A new and better anti-framing option has recently been implemented in some browsers, based on an HTTP Header sent in the response. By configuring this header at the Webserver level, the browser is instructed not to display the response content in a frame or iFrame.
An example implementation of this in an Apache config file is provided in the code examples.  

APIs designed specifically for WebView can be abused to compromise the security of web contents specified inside a WebView. The best way to protect an application and its users against this well-known vulnerability is to:

 * Prevent the X-Frame-Option HTTP response header from loading frames that request content hosted on other domain names. However, this mitigation is not applicable when dealing with a compromised host.
 
 * Leverage internal defense mechanisms to ensure that all UI elements load in top level frames; Thus avoiding serving content through untrusted frames setup at lower levels.
 
## References 

 * [https://developer.mozilla.org/en/The_X-FRAME-OPTIONS_response_header](https://developer.mozilla.org/en/The_X-FRAME-OPTIONS_response_header)

Basic frame busting javascript:

```javascript
if( self != top ) { 
  top.location = self.location ;
}
```

IFrame prevention for server-side Apache config file:

```
Header add X-FRAME-OPTIONS "DENY"
```

Another option is to set this value to “SAMEORIGIN” which will only allow a frame from the same domain. This header has been tested on various browsers including Safari on iOS 4 and confirmed to prevent the display of a page in an iFrame. Provided that no requirements exist for delivery in an iFrame, the recommendation is to use DENY.

## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 20](http://cwe.mitre.org/data/definitions/20.html)
