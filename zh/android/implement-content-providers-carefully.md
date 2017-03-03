# 谨慎使用content providers

## 详细描述 

Content providers 允许应用程序使用URI寻址方案和关系数据库模型共享数据。 它们也可以用于通过URI方案访问文件。

## 建议

Content providers 可以声明权限和单独的读写访问。 除非绝对必要，否则不要给内容提供者写访问权限。 除非必需，请确保设置权限，以便非特权应用程序无法读取`ContentProvider`实例。

将访问限制为操作所需的最低限度。 例如，要与向某个联系人发送该邮件的其他应用程序共享即时消息，只共享该单个邮件，而不是所有即时消息。 内容提供商中的记录级委派功能允许共享特定记录或文件，而不共享整个数据库。 一旦外部应用程序返回到原始应用程序，代表结束。

将传递给内容提供者的参数视为不受信任的输入，并且不在没有防护的情况下直接在SQL查询中使用它们。 没有防护的SQL代码可以通过内容提供者请求发送。 如果SQL代码包含在查询中，它可以返回数据或向攻击者提供控制权。

基于文件名传递给提供者的文件的内容提供者应该确保路径遍历被过滤掉。 例如，如果攻击者在请求中包含`../../../ file'，它可能导致程序读取并返回攻击者在其他情况下不能访问的文件中的数据。 应用程序。 此外，请注意，攻击者创建的以下符号链接可能具有类似的结果。

## CWE/OWASP

 * [M7 - Client Side Injection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M7)
 * [CWE 926: Improper Export of Android Application Components](http://cwe.mitre.org/data/definitions/926.html)
