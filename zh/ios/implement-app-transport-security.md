# 应用ATS(App Transport Security)

## 详细描述 

iOS 9中的新功能，ATS(App Transport Security)有助于确保应用程序和任何后端服务器之间的安全连接。 默认情况下，当应用程序与iOS 9.0 SDK或更高版本链接时，它会启用。 启用ATS后，HTTP连接将强制使用HTTPS（TLS v1.2），并且使用不安全HTTP连接的任何尝试都将失败。

应用ATS包括几个方案：

* 开发人员可以 *启用* 全局ATS（通过链接到iOS 9.0或更高版本的SDK），然后选择使用例外减少特定服务器上的ATS限制
* 开发人员可以 *禁用* 全局ATS（通过将NSAllowsArbitraryLoads键设置为YES），然后使用例外来增加特定服务器上的ATS限制

## 建议

对于在iOS 9.0或更高版本上运行的应用程序，最佳做法是通过链接到iOS 9.0或更高版本的SDK来启用ATS，并且*不要*将`NSAllowsArbitraryLoads`键设置为“Yes”或“True”。 苹果目前允许开发人员为任何不能实施TLS的域设置为例外。 可以使用`NSExceptionAllowsInsecureHTTPLoads`或`NSThirdPartyExceptionAllowsInsecureHTTPLoads`键来设置例外。 重要的是要注意，从2017年1月开始，苹果将要求开发人员对应用程序中声明的任何异常（在App Store审核期间）提供合理的理由。 否则，所有通信必须使用ATS。
## 参考

 * [App Transport Security REQUIRED January 2017](https://forums.developer.apple.com/thread/48979)
 * [Getting Ready for ATS Enforcement in 2017](https://nabla-c0d3.github.io/blog/2016/08/14/ats-enforced-2017/)
 * [Android buckles down and iOS opens up? Trends in platform security affecting developers](https://www.nowsecure.com/blog/2016/08/24/android-buckles-ios-opens-trends-platform-security-affecting-developers/)
 * [iOS 10 Security Changes Slide Deck](https://nabla-c0d3.github.io/blog/2016/09/19/ios10-slide-deck/)
 * [As of December, 2016, only 20 percent of apps enable ATS](https://www.nowsecure.com/blog/2016/12/29/enable-ios-app-transport-security-ats/)
 
## CWE/OWASP 

 * OWASP Mobile Top 10: [M3 - Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * CWE: [CWE-319 - Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
 
