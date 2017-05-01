# 避免敏感数据的查询字符串

## 详细描述

一个主要的突破口是执行一个简单的经过修改过的查询字符串。查询字符串参数是可见的，并且可能经常意外地缓存（从网络历史记录，Web服务器或代理日志等）。应该避免使用未加密的有意义的数据作为查询字符串。 如果用户凭证作为查询字符串参数传输，而不是在POST请求的正文中传输，那么这些凭证可能会被记录在各种地方 - 例如，在用户的浏览器历史记录中，在Web服务器日志中，以及在日志中或者在基础设施服务商采用的任何反向代理。 如果攻击者成功地获得这些资源中的任何一个，则他可以通过捕获存储在那里的用户凭证来提升权限。

## 建议 

使用安全的具有XSRF令牌保护的POST方法来发送用户数据。 在可以找到查询字符串数据的区域中，默认情况下不会记录POST数据。 无论是POST还是GET，都应使用临时会话Cookie。 使用非零初始化向量和临时会话密钥加密数据也可以帮助防止重放攻击。 如果需要，可以使用在主机之间使用安全算法（例如Diffie-Hellman）协商的临时会话密钥来加密查询字符串数据。

## 参考

Pinto, Marcus (2007). The Web Application Hacker’s Handbook: Discovering and Exploiting Security Flaws (Kindle Locations 2813-2816). Wiley. Kindle Edition.

## CWE/OWASP 

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2), [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 598](http://cwe.mitre.org/data/definitions/316.html)
