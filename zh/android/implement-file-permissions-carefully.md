# 谨慎配置 File Permissions

## 详细描述

所有人可读的文件可以作为程序的一个向量，泄漏敏感信息。 所有人可写文件可能会暴露您的应用程序，让攻击者通过覆盖您的应用从存储读取的数据影响其行为。 示例包括设置文件和存储的登录信息。

## 建议

不要创建具有MODE_WORLD_READABLE或MODE_WORLD_WRITABLE权限的文件，除非它是必需的，因为任何应用程序都能读取或写入该文件，即使它可能存储在应用程序的私人数据目录中。

_注意: 这些常量在Android API级别17中已弃用。参考: [http://developer.android.com/reference/android/content/Context.html](http://developer.android.com/reference/android/content/Context.html)_

不要使用chmod二进制或系统调用接受文件模式（chmod，fchmod，creat等）的模式，例如0666,0777和0664，

## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2)
 * [CWE 280](http://cwe.mitre.org/data/definitions/280.html)
