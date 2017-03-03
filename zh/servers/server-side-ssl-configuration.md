# 正确配置服务器端SSL

## 详细描述 

许多Web服务器允许较低的加密设置，例如非常弱的导出级40位加密。 实施强密码套件以保护用于创建共享密钥，在客户端和服务器之间加密消息，以及生成消息哈希和签名以确保这些消息的完整性的信息。 还要确保禁用弱协议。

## 建议

确保正确安装和配置SSL证书以实现最高的加密。 如果可能，仅启用强密码（128位及以上）。

TLSv1已超过10年，并且在2009年被发现很容易受到“重新协商攻击”。

* 大多数使用TLSv1的服务器已修补以关闭此漏洞，但您应针对相关服务器验证此漏洞。
* TLSv1协议已更新，当前更多的TLSv1.2提供了最新的技术和最强的加密密码。 更新到较新版本的TLS应该更加坚固和面向未来的应用程序。

避免使用弱cipher，例如：

* NULL cipher suite
* 匿名Diffie-Hellman
* DES 和 RC4 (因为它们容易受到加密分析攻击)

避免弱协议，例如：

* SSLv2
* SSLv3 (因为容易受到POODLE攻击 - [CVE-2014-3566](https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2014-3566))
* TLS 1.0及以下（因为协议容易受到CRIME和BEAST攻击 - [CVE-2012-4929](http://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2012-4929) 和 [CVE-2011-3389](https://cve.mitre.org/cgi-bin/cvename.cgi?name=cve-2011-3389))

如需获取有关如何安全地设计和配置应用程序的传输层安全性的更多信息。参考 OWASP [Transport Layer Protection Cheat Sheet](https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet) for more information about how to securely design and configure transport layer security for an app.

## 参考 

* [Why Android SSL was downgraded from AES256-SHA to RC4-MD5 in late 2010](http://op-co.de/blog/posts/android_ssl_downgrade/) - http://op-co.de/blog/posts/android_ssl_downgrade/

## CWE/OWASP

 * OWASP Mobile Top 10: [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * CWE: [CWE-326 - Inadequate Encryption Strength](http://cwe.mitre.org/data/definitions/326.html)
