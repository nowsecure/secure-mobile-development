# 保护应用程序服务

## 详细描述 

服务通常用于后台处理。 与BroadcastReceivers和应用程序 activities 一样，应用程序服务可以由外部应用程序调用，因此应该由权限和导出标志保护。

## 建议

服务可以具有可以从外部调用者调用的多于一个方法。 可以为每个方法定义任意权限，并通过使用`checkPermission（）`检查调用包是否具有相应的权限。 或者，可以通过使用AndroidManifest中定义的权限来定义单独的服务和访问权限。

当调用具有敏感数据的服务时，验证正在调用正确的服务，而不是恶意服务。 如果您知道要连接的组件的确切名称，请在用于连接的意图中指定该名称。 另一种方法是再次使用`checkPermission()`来验证调用包是否具有接收所需Intent所需的权限。 用户在安装期间向应用程序授予权限。

下面是一个例子，声明并需要在访问`com.example.MyService.`时使用自定义权限

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
