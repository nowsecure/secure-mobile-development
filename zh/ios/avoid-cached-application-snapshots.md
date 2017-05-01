# 避免缓存应用程序快照

## 详细描述 

为了提供界面中的视觉过渡，iOS会将屏幕截图作为图像存储在设备NAND闪存的文件系统部分中。 当应用程序暂停（而不是终止）时，当按下Home按钮或电话呼叫或其他事件暂时挂起应用程序时，会发生这种情况。 这些图像通常可以包含用户和应用程序数据。 在一个已发布的案例中，它们包含用户的全名，DOB，地址，雇主和信用评分。

## 建议

要保护敏感数据，请使用API配置或代码阻止应用程序快照的缓存。

当applicationDidEnterBackground：方法运行结束时，iOS将采用应用程序用户界面的快照，并且它用于转换动画并存储在文件系统中。 应该重载此方法，并且在返回之前应删除用户界面中的所有敏感信息。 这样快照就不会包含它们。

## 参考

 * [Managing Your Applications Flow][1]
 
## CWE/OWASP 

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4); [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
 
<!-- Links -->
[1]: https://developer.apple.com/library/iOS/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/ManagingYourApplicationsFlow/ManagingYourApplicationsFlow.html#//apple_ref/doc/uid/TP40007072-CH4-SW47
