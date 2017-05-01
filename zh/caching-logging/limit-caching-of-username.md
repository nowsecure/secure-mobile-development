# 限制缓存用户名

## 详细描述 

在iOS上，当用户启用“保存此用户ID”功能时，用户名将缓存在CredentialsManager对象中。 在运行时，用户名在任何类型的身份验证之前加载到内存中，从而允许恶意进程拦截用户名。

## 建议

很难同时向用户提供保存的用户名的便利，以及避免通过不安全的存储或在运行时的潜在拦截来泄露用户名。 虽然不像密码那么敏感，但是用户名是应该保护的私人数据。 提供具有更高安全性的高速缓存用户名选项的一种潜在方法是存储掩蔽的用户名而不是实际的用户名，并且在认证中将用户名值替换为哈希值。 可以创建哈希值，包括在注册时存储的唯一设备令牌。 使用散列和设备令牌的进程的好处是，实际用户名不存储在本地或不加保护地加载到内存中，并且复制到另一个设备或在网络上使用的值将不够。 恶意用户必须发现更多信息才能成功窃取认证用户名。
 
## 参考

 * [http://resources.infosecinstitute.com/ios-application-security-part-20-local-data-storage-nsuserdefaults-coredata-sqlite-plist-files/](http://resources.infosecinstitute.com/ios-application-security-part-20-local-data-storage-nsuserdefaults-coredata-sqlite-plist-files/)

## CWE/OWASP 

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2); [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 312](http://cwe.mitre.org/data/definitions/312.html), [313](http://cwe.mitre.org/data/definitions/313.html), [522](http://cwe.mitre.org/data/definitions/522.html)
