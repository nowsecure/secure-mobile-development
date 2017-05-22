# 7.14 Set the "usesCleartextTraffic" flag to false

## Details

An unsecured communications channel between an app and any back-end services can expose the data transmitted between them. Similar to the App Transport Security (ATS) feature in iOS (see also best practice [6.5 Implement App Transport Security](https://books.nowsecure.com/secure-mobile-development/en/ios/implement-app-transport-security.html)), Android 6.0 and later makes it easier to prevent an app from using cleartext network traffic (e.g., HTTP and FTP without TLS) by adding the `android:usesCleartextTraffic` attribute to the Android Manifest.

## Remediation

Set the `usesCleartextTraffic` flag to false in the Android Manifest. This will result in the app asking the platform and third-party libraries to prevent the app from using cleartext traffic.

* Not all APIs will honor the flag, however, and developers/security analysts will need to determine what APIs will or will not honor the flag.

* Also note that WebView will not honor the `usesCleartextTraffic` flag (if you must use WebView, see also best practice [7.9 - Follow WebView Best Practices](https://github.com/nowsecure/secure-mobile-development/blob/master/en/android/webview-best-practices.md)). 

* If specific services used by the app require cleartext, developers can use the Network Security Configuration feature (`android:networkSecurityConfig`) to manually add exceptions if absolutely necessary.

## CWE/OWASP

* OWASP Mobile Top 10: [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M3-Insecure_Communication)
* CWE: [CWE-319 - Cleartext Transmission of Sensitive Information](https://cwe.mitre.org/data/definitions/319.html)
