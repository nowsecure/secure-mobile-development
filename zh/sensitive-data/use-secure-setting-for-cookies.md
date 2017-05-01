# 使用Cookie的安全设置

## 详细描述 

如果Cookie未标记为“Secure”，则无论与主机的会话是否安全，都可能通过不安全的连接进行传输。 换句话说，它可以通过HTTP连接来传输。

此外，由于Cookie无法通过客户端访问（例如，无法使用JavaScript代码段访问），因此在Cookie上设置“HTTPOnly”标志可防止跨站点脚本（XSS）等攻击。

## 建议

Set-Cookie头应该使用“Secure”和“HTTPOnly”设置。 这些设置应适用于本机和/或网络应用程序的所有Cookie。

## CWE/OWASP 

 * OWASP Mobile Top 10: [M9 - Improper Session Handling](https://www.owasp.org/index.php/Mobile_Top_10_2014-M9)
 * CWE [CWE-614 - Sensitive Cookie in HTTPS Session Without 'Secure' Attribute](http://cwe.mitre.org/data/definitions/79.html)
 
