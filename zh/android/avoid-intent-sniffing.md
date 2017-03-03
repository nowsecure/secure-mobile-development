# 避免 Intent 嗅探

当activity由另一个使用广播Intent的应用程序启动时，Intent中传递的数据可以由恶意应用程序读取。

## 详细描述 

当另一个应用程序通过发送广播Intent启动activity时，恶意应用程序可以读取Intent中包含的数据。 恶意应用程序还可以读取应用程序的最近Intent列表。 例如，如果应用程序调用并传递URL到Android Web浏览器，攻击者可以嗅探该URL。

## 建议

不要在使用广播Intent的应用之间传递敏感数据。 而使用显式Intent。

## CWE/OWASP

 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE 285: Improper Authorization](http://cwe.mitre.org/data/definitions/285.html)
