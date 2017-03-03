# 谨慎使用 Broadcasts

## 详细描述 

如果在发送广播Intent时未设置权限，则任何非特权应用程序都可以接收Intent，除非它有明确的目标。

攻击者可以通过以下方式利用没有任何设置权限的Intent：

- 创建包含与合法组件具有相同名称的组件的恶意应用程序
- 只要该名称（或命名空间）尚未使用，恶意应用程序将安装在目标设备上
- 从发送到该组件名称的广播Intent提取敏感数据

## 建议

使用权限来保护应用程序中的Intents。 请记住，当通过广播Intent向第三方组件发送信息时，该组件可能已被恶意安装替换。

## 参考 

 * [https://developer.android.com/training/articles/security-tips.html#Permissions](https://developer.android.com/training/articles/security-tips.html#Permissions)
 * [http://shop.oreilly.com/product/0636920022596.do](http://shop.oreilly.com/product/0636920022596.do)

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE-925: Improper Verification of Intent by Broadcast Receiver](http://cwe.mitre.org/data/definitions/925.html)
