# 保护内部资源

## 详细描述 

用于内部使用的资源（例如管理员登录表单）经常使用可能被暴力破解的身份验证。 例如无锁定的HTTP或表单认证。 管理或其他内部资源的泄露可能导致广泛的数据丢失和其他损害。

## 建议

这种资源应该被阻止外部访问。 任何不需要公共互联网访问的资源都应该使用防火墙规则和网络分段进行限制。 如果登录页面，管理区域或其他资源是外部可访问的，它就会被恶意用户发现和暴力攻击。

## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 200 - Multiple CWE's](http://cwe.mitre.org/data/definitions/200.html)
