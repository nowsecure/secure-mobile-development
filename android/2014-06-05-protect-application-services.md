---
layout: guide
title: "Protect Application Services"
description: "Services are typically used for background processing."
published: 1
categories:
  - android
series:
  name: Android
  index: 9
order: 606
--- 

## Details 

Services are typically used for background processing. Similar to Activities and Broadcast Receivers, Services can be invoked by external applications and should be protected by permissions and export flags as appropriate.

## Remediation

A service may have more than one method which can be invoked from an external caller. It is possible to define arbitrary permissions for each method and check if the calling package has the corresponding permission by using `checkPermission()`. Alternatively, one could define separate services and secure access through the use of permissions defined in the AndroidManifest.

When calling a service with sensitive data, one may need to validate the service is the correct one and not a malicious service. If you know the exact name of the component you are trying to connect to you can specify that in the Intent used to connect. Otherwise one can use `checkPermission()` again to verify if the calling package has the particular permission needed to receive the desired Intent. It is up to the user at installation-time to grant the permission to the app.

Here is an example where a custom permission is declared and required to be used when accessing the `com.example.MyService.`

```xml
<permission android:name="com.example.mypermission" 
android:label="my_permission" android:protectionLevel="dangerous"></permission>`
```
```xml
<service

	android:name="com.example.MyService"
	
	android:permission="com.example.mypermission">
	
	<intent-filter>
	
		<action android:name="com.example.MY_ACTION" />
		
	</intent-filter>
		
</service>
```

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 280](http://cwe.mitre.org/data/definitions/280.html)
