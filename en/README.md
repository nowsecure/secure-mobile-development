# Secure Mobile Development

At NowSecure we spend a lot of time attacking mobile apps - hacking, breaking encryption, finding flaws, penetration testing, and looking for sensitive data stored insecurely. We do it for the right reasons - to help developers make their apps more secure. This document represents some of the knowledge we share with our clients and partners. **We are driven to advance mobile app security worldwide.**

## Using this Guide

This guide gives specific recommendations to use during your development process. The descriptions of attacks and security recommendations in this report are not exhaustive or perfect, but you will get practical advice that you can use to make your apps more secure.

We revise our best practices periodically and invite [contributions](https://github.com/nowsecure/secure-mobile-development/pulls), and the updated guide is published [here](https://books.nowsecure.com/secure-mobile-development/) as changes are accepted into the main repository.

To learn about all the vectors that attackers might use on your app, read our [Mobile Security Primer](primer/mobile-security.md).

### Table of Contents

* [Mobile Security Primer](primer/mobile-security.md)
* [Coding Practices](coding-practices/README.md)
  * [2.1 Increase Code Complexity and Use Obfuscation](coding-practices/code-complexity-and-obfuscation.md)
  * [2.2 Avoid Simple Logic](coding-practices/avoid-simple-logic.md)
  * [2.3 Test Third-Party libraries](coding-practices/test-third-party-libraries.md)
  * [2.4 Implement Anti-tamper Techniques](coding-practices/anti-tamper-techniques.md)
  * [2.5 Securely Store Sensitive Data in RAM](coding-practices/securely-store-sensitive-data-in-ram.md)
  * [2.6 Understand Secure Deletion of Data](coding-practices/understand-secure-deletion-of-data.md)
  * [2.7 Avoid Query String for Sensitive Data](coding-practices/avoid-query-string-for-sensitive-data.md)
* [Handling Sensitive Data](sensitive-data/README.md)
  * [3.1 Implement Secure Data Storage](sensitive-data/implement-secure-data-storage.md)
  * [3.2 Use SECURE Setting For Cookies](sensitive-data/use-secure-setting-for-cookies.md)
  * [3.3 Fully validate SSL/TLS](sensitive-data/fully-validate-ssl-tls.md)
  * [3.4 Protect Against SSL Downgrade Attacks](sensitive-data/protect-against-sslstrip.md)
  * [3.5 Limit Use of UUID](sensitive-data/limit-use-of-uuid.md)
  * [3.6 Treat Geolocation Data Carefully](sensitive-data/treat-geolocation-data-carefully.md)
  * [3.7 Institute Local Session Timeout](sensitive-data/institute-local-session-timeout.md)
  * [3.8 Implement Enhanced/Two-Factor Authentication](sensitive-data/implement-enhanced-two-factor-authentication.md)
  * [3.9 Protect Application Settings](sensitive-data/protect-application-settings.md)
  * [3.10 Hide Account Numbers and Use Tokens](sensitive-data/hide-account-numbers-and-use-tokens.md)
  * [3.11 Implement Secure Network Transmission Of Sensitive Data](sensitive-data/implement-secure-network-transmission-of-sensitive-data.md)
  * [3.12 Validate Input From Client](sensitive-data/validate-input-from-client.md)
  * [3.13 Avoid Storing App Data in Backups](sensitive-date/avoid-storing-app-data-in-backups.md)
* [Caching and Logging](caching-logging/README.md)
  * [4.1 Avoid Caching App Data](caching-logging/avoid-caching-app-data.md)
  * [4.2 Avoid Crash Logs](caching-logging/avoid-crash-logs.md)
  * [4.3 Limit Caching of Username](caching-logging/limit-caching-of-username.md)
  * [4.4 Carefully Manage Debug Logs](caching-logging/carefully-manage-debug-logs.md)
  * [4.5 Be Aware of the Keyboard Cache](caching-logging/be-aware-of-the-keyboard-cache.md)
  * [4.6 Be Aware of Copy and Paste](caching-logging/be-aware-of-copy-paste.md)
* [Webviews](webviews/README.md)
  * [5.1 Prevent Framing and Clickjacking](webviews/prevent-framing-and-clickjacking.md)
  * [5.2 Protect against CSRF with form tokens](webviews/protect-against-csrf-with-form-tokens.md)
* [iOS](ios/README.md)
  * [6.1 Use the Keychain Carefully](ios/use-the-keychain-carefully.md)
  * [6.2 Avoid Cached Application Snapshots](ios/avoid-cached-application-snapshots.md)
  * [6.3 Implement Protections Against Buffer Overflow Attacks](implement-protections-against-buffer-overflow-attacks.md)
  * [6.4 Avoid Caching HTTP(S) Requests/Responses](ios/avoid-caching-https-requests-responses.md)
  * [6.5 Implement App Transport Security (ATS)](ios/implement-app-transport-security.md)
  * [6.6 Implement Touch ID Properly](implement-touch-id-properly.md)
* [Android](android/README.md)
  * [7.1 Implement File Permissions Carefully](android/implement-file-permissions-carefully.md)
  * [7.2 Implement Intents Carefully](android/implement-intents-carefully.md)
  * [7.3 Check Activities](android/check-activities.md)
  * [7.4 Use Broadcasts Carefully](android/use-broadcasts-carefully.md)
  * [7.5 Implement PendingIntents Carefully](android/implement-pendingintents-carefully.md)
  * [7.6 Protect Application Services](android/protect-application-services.md)
  * [7.7 Avoid Intent Sniffing](android/avoid-intent-sniffing.md)
  * [7.8 Implement Content Providers Carefully](android/implement-content-providers-carefully.md)
  * [7.9 Follow WebView Best Practices](android/webview-best-practices.md)
  * [7.10 Avoid Storing Cached Camera Images](android/avoid-storing-cached-camera-images.md)
  * [7.11 Avoid GUI Objects Caching](android/avoid-gui-objects-caching.md)
  * [7.12 Sign Android APKs](android/android-apk-signing.md)
* [Servers](servers/README.md)
  * [8.1 Implement Proper Web Server Configuration](servers/web-server-configuration.md)
  * [8.2 Properly Configure Server-side SSL](servers/server-side-ssl-configuration.md)
  * [8.3 Use Proper Session Management](servers/web-servers-proper-session-management.md)
  * [8.4 Protect and Perform Penetration Testing of Web Services](servers/protect-and-pen-test-web-services.md)
  * [8.5 Protect Internal Resources](servers/protect-internal-resources.md)
