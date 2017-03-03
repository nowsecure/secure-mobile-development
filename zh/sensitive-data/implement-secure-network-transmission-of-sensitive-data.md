# 使用安全的网络传输方法传输敏感数据

## 详细描述 

与网络浏览器不同，移动设备通常不会公开应用程序是否使用SSL / TLS来保护数据传输，因此应用程序用户只能相信应用程序的开发人员已实施网络加密。

多年来，SSL（后继者是TLS）一直是Web通信加密的标准，包括为移动应用程序提供支持的Web服务。 然而，违反认证机构如DigiNotar和Comodo暴露了许多用户伪造证书。 苹果 “[goto fail](https://avandeursen.com/2014/02/22/gotofail-security/)” 错误进一步暴露了SSL / TLS的可靠性依赖于应用程序开发人员。

今天，最佳实践要求应用提供商有效地使用SSL / TLS来保护通过网络传输密码，登录ID和其他敏感数据，甚至进一步利用应用层加密来保护用户数据。

## 建议

使用SSL / TLS与标准信任验证，或为了增加安全性，实施证书锁定(参考 3.3 [完全验证SSL / TLS](fully-validate-ssl-tls.md) 以及 OWASP “[Pinning Cheat Sheet](https://www.owasp.org/index.php/Pinning_Cheat_Sheet)”).

为了防止通过受损的SSL / TLS连接拦截高度敏感的值（例如登录ID，密码，PIN，帐号等），请在传输过程中增加额外的加密。 使用密钥大小256为AES（也称为Rijndael）加密高度敏感的值。而对于hash，请使用诸如SHA-256或更高版本的算法。

在服务器端，请考虑仅接受强TLS密码和密钥，并禁用较低级别的加密，例如导出级40位加密 (参考 8.2 [正确配置服务器端SSL](../servers/server-side-ssl-configuration.md)) 

## CWE/OWASP 

 * OWASP Mobile Top 10: [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * CWE: [CWE-311 - Missing Encryption of Sensitive Data](http://cwe.mitre.org/data/definitions/311.html), [CWE-319 - Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
