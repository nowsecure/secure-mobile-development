# Protect Application Services

## Details 

Services are typically used for background processing. Like BroadcastReceivers and application activities, application services can be invoked by external applications and so should be protected by permissions and export flags.

## Remediation

A service may have more than one method which can be invoked from an external caller. It is possible to define arbitrary permissions for each method and check if the calling package has the corresponding permission by using `checkPermission()`. Alternatively, one could define separate services and secure access through the use of permissions defined in the AndroidManifest.

When calling a service with sensitive data, validate that the correct service is being called and not a malicious service. If you know the exact name of the component to which you wish to connect, specify that name in the Intent used to connect. Another method is to use `checkPermission()` again to verify whether the calling package has the permissions required to receive the desired Intent. The user grants permissions to the app during installation.

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
 * [CWE-280: Improper Handling of Insufficient Permissions or Privileges](http://cwe.mitre.org/data/definitions/280.html)
