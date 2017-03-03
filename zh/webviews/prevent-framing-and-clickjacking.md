# 防止frame劫持和点击劫持

## 详细描述 

Frame劫持涉及在iFrame中传送Web / WAP站点。 这种攻击可以使“包装”站点执行点击劫持攻击。 点击劫持是一个非常真实的威胁，已被利用高信息服务（例如Facebook）窃取信息或重定向用户到攻击者控制的网站。

Frame劫持的主要目的是诱骗用户点击不同的东西，他们的意图。 目标是通过链接漏洞（如跨站脚本）收集机密信息或控制受影响的计算机。 这种攻击通常采用嵌入在源代码中的脚本的形式，该脚本在用户不知道的情况下执行。 当用户单击看起来执行其他功能的按钮时，可以触发。

## 建议

在iOS中防止这种做法的最好方法是不使用WebViews。 非常非常小心的使用

``` 
- (NSString *)stringByEvaluatingJavaScriptFromString:(NSString *)script
```

[(click here for more info on the NSString Class Reference)](https://developer.apple.com/library/ios/documentation/Cocoa/Reference/Foundation/Classes/NSString_Class/Reference/NSString.html#//apple_ref/doc/c_ref/NSString).

防止Frame劫持的一种机制利用客户端JavaScript。 大多数网站已经不能离开JavaScript，因此在JavaScript中实现安全措施（和禁用没有它的网站）是一个方案。 虽然客户端不是不能被篡改，但是这方案确实提高了攻击者的标准。 下面是一个JavaScript代码示例，它强制网站到“顶部”框架，从而“破坏”已加载网站的框架。

攻击者可以添加一些额外的代码来防止Frame劫持被破坏，例如在Frame unload时提醒用户不要退出。 更复杂的JavaScript可能能够对抗这样的技术。 但是包含Frame劫持破坏代码使得简单的Frame劫持变得困难。

**X-FRAME-OPTIONS HEADER**– 最近在一些浏览器中基于响应中的HTTP头实现了一种新的更好的反frame 劫持方案。 通过在Webserver级别配置此HTTP头，指示浏览器不在Frame或iFrame中显示响应内容。在代码示例中提供了Apache配置文件中的示例实现。

专门为WebView设计的API可能被滥用来危害WebView中指定的Web内容的安全性。 保护应用程序及其用户免受这个众所周知的漏洞的最佳方法是：

 * 防止X-Frame-Option HTTP响应头加载请求其他域名托管的内容的框架。 但是，这种方案不适用于处理受影响的主机。
 
 * 利用内部防御机制，确保所有UI元素在顶层框架中加载; 这样就避免了在较低的层次，通过不信任的Frame展示内容。
 
## 参考 

 * [https://developer.mozilla.org/en/The_X-FRAME-OPTIONS_response_header](https://developer.mozilla.org/en/The_X-FRAME-OPTIONS_response_header)

基本Frame破解javascript：

```javascript
if( self != top ) { 
  top.location = self.location ;
}
```

服务器端Apache配置文件的反iframe方案：

```
Header add X-FRAME-OPTIONS "DENY"
```
另一个选项是将此值设置为“SAMEORIGIN”，它将只允许来自相同域的Frame。 此标题已在各种浏览器上测试，包括iOS 4上的Safari，并确认可防止在iFrame中显示页面。 如果在iFrame中没有传送要求，建议使用DENY。

## CWE/OWASP

 * [M1 - Weak Server Side Controls](https://www.owasp.org/index.php/Mobile_Top_10_2014-M1)
 * [CWE 20](http://cwe.mitre.org/data/definitions/20.html)
