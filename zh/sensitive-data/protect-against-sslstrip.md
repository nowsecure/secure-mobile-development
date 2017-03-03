# 防止SSL降级攻击

## 详细描述

使用这种形式的中间人攻击，攻击者可以通过透明地劫持网络上的HTTP流量，监控HTTPS请求，然后消除SSL / TLS来绕过SSL / TLS，从而在客户端和服务器之间创建不安全的连接。 这种攻击在移动网络应用上尤其难以预防（移动网络应用本质上是一个看起来像应用的网页）。

## 建议

通过TLS提供所有流量，甚至非敏感流量。 这防止了任何可能的降级/剥离攻击，因为攻击者需要初始明文“入口点”来完成所述攻击。

验证SSL / TLS是否处于活动状态。 在完全本机应用程序中验证SSL / TLS是相对简单的。 移动网络应用可以通过JavaScript验证SSL / TLS，以便如果未检测到HTTPS连接，则客户端将重定向到HTTPS。 要求SSL / TLS的更可靠的手段是HTTP严格传输安全（HSTS）头。 HSTS标头强制与该域的所有后续连接使用TLS和原始证书。 浏览器只是开始实现HSTS头而移动浏览器总是滞后。

在应用程序中使用图标或语言，以确保用户在所述连接不依赖于经过验证的HTTPS会话时知道并进行安全连接。 教育用户是降低SSL / TLS降级攻击风险的重要组成部分。 在应用程式内使用弹出提示和文字提示，强化使用者使用HTTPS保护网路流量的重要性。

最近在Android和iOS中实施的另一种缓解措施是将非TLS /纯文本流量视为开发人员错误。Android最近添加 `android:usesCleartextTraffic` ([Android M and the War on Cleartext Traffic](https://koz.io/android-m-and-the-war-on-cleartext-traffic/)，而iOS 9及更高版本要求您手动添加明文流量的例外。 替换Web协议HTTP / 2是另一个未来的解决方案，因为它仅使用TLS（并且包括其他功能）.

## 参考

* [Moxie Marlinspike’s sslstrip exploitation tool](https://moxie.org/software/sslstrip/) - https://moxie.org/software/sslstrip/

## CWE/OWASP

 * OWASP Mobile Top 10: [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * CWE: [CWE-757: Selection of Less-Secure Algorithm During Negotiation ('Algorithm Downgrade')](http://cwe.mitre.org/data/definitions/757.html)


