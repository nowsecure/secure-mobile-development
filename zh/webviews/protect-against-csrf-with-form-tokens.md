# 使用表单令牌保护CSRF

## 详细描述 

CSRF (Cross-site Request Forgery) 依赖于已知或可预测的表单值和登录的浏览器会话。

## 建议

每个表单提交应包含一个令牌，该令牌在表单中或在用户会话的开头载入。 在接收POST请求时，在服务器上检查此令牌，以确保是用户启动它。 此功能已经被主流Web平台提供，仅需要少量定制表单开发。

## 参考 

 * [http://op-co.de/blog/posts/android_ssl_downgrade/](http://op-co.de/blog/posts/android_ssl_downgrade/)

## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 325](http://cwe.mitre.org/data/definitions/325.html)
