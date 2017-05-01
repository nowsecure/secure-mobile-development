# 验证来自客户端的输入

## 详细描述 

即使数据是从您的应用程序生成的，这些数据也可能被拦截和操纵。 这可能包括导致应用程序崩溃（生成关键崩溃日志），缓冲区溢出，SQL注入和其他攻击的攻击。 通过实现UITextFieldDelegate中的方法并利用上面的建议，这可以很容易地在iOS中执行。
 
## 建议

与正确的Web应用程序安全性一样，客户端的所有输入都必须被视为不受信任。 服务必须彻底过滤和验证应用程序和用户的输入。 适当的清理包括在发送之前和接收期间的所有用户输入。

## References 

 * iOS
	[https://developer.apple.com/library/ios/documentation/uikit/reference/UITextFieldDelegate_Protocol/UITextFieldDelegate/UITextFieldDelegate.html](https://developer.apple.com/library/ios/documentation/uikit/reference/UITextFieldDelegate_Protocol/UITextFieldDelegate/UITextFieldDelegate.html)	
 * Android - Content Provider Injection Case of Study - 
	[https://viaforensics.com/mobile-security/ebay-android-content-provider-injection-vulnerability.html](https://viaforensics.com/mobile-security/ebay-android-content-provider-injection-vulnerability.html)
	
## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8)
 * [CWE 79](http://cwe.mitre.org/data/definitions/79.html), [89](http://cwe.mitre.org/data/definitions/89.html), [120](http://cwe.mitre.org/data/definitions/120.html)
 
