# 在内存中安全的存储敏感数据

通常，iOS开发人员会将应用程序设置存储在plist文件中，在某些情况下这可能会受到影响。

## 详细描述 

当应用程序正在使用时，用户或应用程序特定的数据可以存储在RAM中，并且在用户注销或会话超时时不会正确清除。 因为Android将应用程序存储在内存中（即使在使用后），直到内存被回收，加密密钥可能会保留在内存中。 发现或窃取设备的攻击者可以附加调试器并从应用程序转储内存，或者加载内核模块以转储内存中的全部内容。

当管理密码和其他敏感信息时，应用程序会将该信息保存在内存中，即使缓冲区释放了一段时间。 如果应用程序容易出现缓冲区溢出，格式化字符串，数据泄露和其他漏洞，这可能是一个安全问题，这可能允许攻击者转储进程的内存以恢复敏感信息。

## 建议

不要将内存中保存敏感数据（例如加密密钥）长于所需的时间。 清除使用后保存密钥的任何变量。 避免对敏感的密钥或密码使用不可变对象，如在Android`java.lang.String`中，而是使用char数组。 即使对不可变对象的引用被删除或清空，它们可能保留在内存中，直到垃圾回收发生（这不能被应用程序强制）。

这只能通过低级语言完成，因为如果优化例程检测到缓冲区在覆盖后不再使用，编译器和即时虚拟机将会因性能原因而忽略这些操作。

有一些工具可以来绕过编译器优化以清除这些缓冲区，但他们都依赖工具链，特定的语言和平台。

## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE-316: Cleartext Storage of Sensitive Information in Memory](http://cwe.mitre.org/data/definitions/316.html)
 * [CWE-200: Information Exposure](http://cwe.mitre.org/data/definitions/200.html)
 * [CVE-2014-0160 Heartbleed](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0160)
