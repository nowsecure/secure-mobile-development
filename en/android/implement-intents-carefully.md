# Implement Intents Carefully

## Details

Intents are used for inter-component signaling and can be used

 * *To start an Activity, typically opening a user interface for an app*
 * *As broadcasts to inform the system and apps of changes*
 * *To start, stop, and communicate with a background service*
 * *To access data via ContentProviders*
 * *As callbacks to handle events*

Improper implementation could result in data leakage, restricted functions being called and program flow being manipulated.

## Remediation

 * Components accessed via Intents can be public or private. The default is dependent on the intent-filter and it is easy to mistakenly allow the component to be or become public. It is possible to set component as android:exported=false in the app’s Manifest to prevent this.

 * Public components declared in the Manifest are by default open so any application can access them. If a component does not need to be accessed by all other apps, consider setting a permission on the component declared in the Manifest.

 * Data received by public components cannot be trusted and must be scrutinized.

## CWE/OWASP

 * [M1 - Improper Platform Usage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M1-Improper_Platform_Usage), [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * [CWE 927](http://cwe.mitre.org/data/definitions/316.html)
* [Android: Access to app protected components](https://blog.oversecured.com/Android-Access-to-app-protected-components/)
