# 使用合适的会话管理

## 详细描述 

大多数应用程序都通过可能容易受到攻击的Cookie来维护用户的会话。

## Remediation

Web语言（例如Java，.NET）提供会话管理，这是经过良好开发和安全测试的。 使服务器软件保持最新的安全补丁。 开发您自己的会话管理更有风险，只有在适当的专业知识。 确保会话cookie的大小足够。 短的或可预测的会话cookie使攻击者可能预测，高压或对会话执行其他攻击。 在会话配置中使用高安全性设置。

## CWE/OWASP

 * [M9 - Improper Session Handling](https://www.owasp.org/index.php/Mobile_Top_10_2014-M9)
 * [CWE 613](http://cwe.mitre.org/data/definitions/613.html)
