# 保护和执行Web服务的渗透测试

## 详细描述 

已经被攻破的服务器有可能拦截用户凭据并对应用用户发起其他攻击。

## 建议

一般来说，生产Web服务器必须经过彻底测试和防御恶意攻击。 生产服务器软件应更新到最新版本，并加固以防止有关服务器软件和接口的信息泄露。

身份验证表单不应反映用户名是否存在。 如果攻击者有一个方法来确定有效的用户名，他们有一个起点的暴力攻击和网络钓鱼攻击。 通过向客户端提供“无效的用户/密码组合”和“没有找到此类用户名”事件的相同响应，阻止用户名收集。 所有的交换敏感数据的登录表单和表单/页面都应该实现并需要HTTPS。 Web服务器不应允许没有SSL的客户端连接用于此类资源。 关闭详细错误，删除任何遗留的不必要的站点或页面，并持续强化Web资源以防潜在的攻击。

## 参考 


## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 307](http://cwe.mitre.org/data/definitions/307.html), [200](http://cwe.mitre.org/data/definitions/200.html), etc. (could be multiple)
