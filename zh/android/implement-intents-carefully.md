# 谨慎实现 Intents

## 详细描述 

Intents用于组件间信令，而且可以被用来做以下事情：

 * *启动Activity，通常为应用程序打开用户界面*
 * *作为广播以通知系统和应用程序的变化*
 * *开始，停止和与后台服务进行通信*
 * *通过ContentProvider访问数据*
 * *作为回调处理事件*

不正确的实现可能导致数据泄露，受限功能被调用和程序流被操纵。

## 建议

 * 通过Intents访问的组件可以是公共的或私有的。 默认值取决于Intents过滤器，很容易错误地允许组件被公开。 可以在应用程序的Manifest中将组件设置为`android：exported = false`，以防止出现这种情况。
 
 * 默认情况下，在清单中声明的公共组件是开放的，所以任何应用程序都可以访问它们。 如果组件不需要被所有其他应用程序访问，请考虑设置对清单中声明的组件的权限。

 * 公共组件接收的数据不可信任，必须仔细检查。

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 927](http://cwe.mitre.org/data/definitions/316.html)
