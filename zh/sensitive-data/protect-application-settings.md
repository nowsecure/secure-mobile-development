# 保护应用程序设置

## 详细描述 

iOS开发人员经常将应用程序设置存储在plist文件中，在某些情况下可能会受到损害。 类似地，Android开发人员通常将设置存储在共享首选项XML文件或SQLite数据库中，这些数据库在默认情况下未加密，可以使用root权限读取或甚至修改，或使用备份。

## 建议

尽可能将设置编译为代码。 通过plist文件在iOS上配置应用程序没有什么好处，因为更改必须绑定并部署为新的应用程序。 相反，如果将配置包含在应用程序代码中，攻击者需要更多的时间和技能才能修改。 除非先加密不要在字典或其他文件中存储任何关键设置。 理想情况下，使用由用户提供的密码加密的主密钥或用户登录系统时远程提供的密钥加密所有配置文件。

## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2), [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 312](http://cwe.mitre.org/data/definitions/312.html), [313](http://cwe.mitre.org/data/definitions/313.html)
