# 避免缓存应用程序数据

## 详细描述 

数据可以在很多地方被捕获，尽管许多是无意的。 开发人员经常忽略一些可以存储数据的方式，包括日志/调试文件，cookie，网络历史记录，网页缓存，属性列表，文件和SQLite数据库。 在移动设备上安全地存储数据需要适当的技术。 只要有可能***“简单地不要存储或缓存数据”*** 是避免数据在设备上被获取最直接的方式。

## 建议

阻止HTTP高速缓存。 开发人员可以将iOS和Android配置为不缓存网络数据，特别是HTTPS流量。 在iOS中，查看实现NSURLConnection委托并禁用newCachedResponse。 此外，我们建议采取步骤，以避免缓存任何Web进程（如注册）的URL历史记录和页面数据。 HTTP缓存头在此重要，并在Web服务器上配置。 HTTP协议在响应标头中支持“no-store”指令，指示浏览器它不得存储响应或引发它的请求的任何部分。 对于Web应用程序，HTML表单输入可以使用autocomplete = off设置指示浏览器不缓存值。 应用程序启动后，可以通过对设备数据进行读取检查来验证是否已经缓存了数据。

## 参考

 * [http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html)


## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2), [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 312](http://cwe.mitre.org/data/definitions/312.html), [313](http://cwe.mitre.org/data/definitions/313.html), [522](http://cwe.mitre.org/data/definitions/522.html), [200](http://cwe.mitre.org/data/definitions/200.html)

