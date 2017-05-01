# Follow WebView Best Practices

## Details

WebViews can introduce a number of security concerns and should be implemented carefully. In particular, a number of exploitable vulnerabilities arising from the use of the addJavscriptInterface API have been discovered.

## Remediation

Disable JavaScript and Plugin support if they are not needed. While both are disabled by default, best practices call for explicitly setting them as disabled. Disable local file access. This restricts access to the app’s resource and asset directory and mitigates against an attack from a web page which seeks to gain access to other locally accessible files.

Disallow the loading of content from third-party hosts. This can be difficult to achieve from within the app. However, a developer can override shouldOverrideUrlLoading and shouldInterceptRequest to intercept, inspect, and validate most requests initiated from within a WebView. A developer may also consider implementing a whitelist scheme by using the URI class to inspect components of a URI to ensure it matches an entry within a list of approved resources.

Sample code [https://gist.github.com/scottyab/6f51bbd82a0ffb08ac7a](https://gist.github.com/scottyab/6f51bbd82a0ffb08ac7a)

## References

 * [http://labs.mwrinfosecurity.com/blog/2012/04/23/adventures-with-android-webviews/](http://labs.mwrinfosecurity.com/blog/2012/04/23/adventures-with-android-webviews/)
 * [https://developer.android.com/training/articles/security-tips.html#WebView](https://developer.android.com/training/articles/security-tips.html#WebView)

## CWE/OWASP

 * [M7 - Client Code Quality](https://www.owasp.org/index.php/Mobile_Top_10_2016-M7-Poor_Code_Quality)
 * [CWE-79: Improper Neutralization of Input During Web Page Generation (Cross-site Scripting)](http://cwe.mitre.org/data/definitions/79.html)
