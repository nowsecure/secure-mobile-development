# 谨慎使用keychain

## 详细描述 

iOS提供了安全数据存储的钥匙串。 然而，在几种情况下，钥匙串可能被泄密并随后被解密。

在iOS的所有版本，包括iOS 7，如果攻击者可以访问加密的iTunes备份，钥匙串可能部分破解。 由于iOS在创建iTunes备份时重新加密钥匙串条目的机制，所以当iTunes备份可用且备份加密的密码已知时，钥匙串可以被部分解密。 但是，未加密的iTunes备份不允许解密钥匙串项。

如果越狱已应用于设备，则钥匙串访问控制将无效。 在越狱的情况下，在设备上运行的任何应用程序都可能读取每个其他应用程序的钥匙串项目。

最后，对于存在BootROM漏洞的旧设备（例如，iPhone 4），该钥匙串可能被具有对该设备的物理访问的攻击者获取。
## 建议

当在钥匙串中存储数据时，使用最严格的保护类（由`kSecAttrAccessible`属性定义）仍然允许您的应用程序正常工作。 例如，如果您的应用程序不是设计为在后台运行，请使用`kSecAttrAccessibleWhenUnlocked`或`kSecAttrAccessibleWhenUnlockedThisDeviceOnly`。

要防止通过iTunes备份暴露钥匙串项目，请在实用的情况下使用ThisDeviceOnly 选项。

最后，对于高度敏感的数据，考虑使用应用程序级加密来增强钥匙串提供的保护。 例如，依靠用户输入密码在应用程序内进行认证，然后使用该密码在将数据存储到密钥链之前对数据进行加密。

## 参考
 
 * [Keychain Services Programming Guide][1]
	
## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2); [M5 - Poor Authorization and Authentication](https://www.owasp.org/index.php/Mobile_Top_10_2014-M5)
 * [CWE-312: Cleartext Storage of Sensitive Information](http://cwe.mitre.org/data/definitions/312.html)
 * [CWE-522: Insufficiently Protected Credentials](http://cwe.mitre.org/data/definitions/522.html)

<!-- Links -->
[1]: https://developer.apple.com/library/ios/documentation/security/Conceptual/keychainServConcepts/01introduction/introduction.html#//apple_ref/doc/uid/TP30000897
