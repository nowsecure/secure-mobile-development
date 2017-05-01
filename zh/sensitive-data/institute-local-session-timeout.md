# 本地会话超时机制

## 详细描述 

移动设备经常丢失或被盗，攻击者可以利用活动的会话来访问敏感数据，执行事务或在设备所有者的帐户上执行侦察。 此外，如果没有适当的会话超时，应用可能容易受到中间人攻击的数据拦截。

## 建议

任何时间应用程序不使用超过5分钟，终止活动会话，将用户重定向到登录屏幕，确保没有应用程序数据可见，并要求用户重新输入登录凭据以访问 应用程序。

超时后，还要丢弃和清除与用户数据相关联的所有内存，包括用于解密数据的任何主密钥 (参考 2.5 [在内存中安全的存储敏感数据](../coding-practices/securely-store-sensitive-data-in-ram.md))

此外，确保客户端和服务器端都发生会话超时，以减轻攻击者修改本地超时机制。

## CWE/OWASP 

 * OWASP Mobile Top 10: [M9 - Improper Session Handling](https://www.owasp.org/index.php/Mobile_Top_10_2014-M9)
 * CWE: [CWE-613 - Insufficient Session Expiration](http://cwe.mitre.org/data/definitions/613.html)
 
