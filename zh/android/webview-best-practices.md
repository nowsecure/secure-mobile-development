# 遵循WebView最佳实践

## 详细描述 

WebView可以引入一些安全问题，应该小心地使用。 目前已经发现了使用addJavscriptInterface API所产生的许多可利用的漏洞。

## 建议

如果不需要JavaScript和Plugin支持，请禁用。 虽然默认情况下都禁用它们，但最佳做法需要明确将其设置为禁用。 禁用本地文件访问。 这限制了对应用程序的资源和资产目录的访问，并减轻了来自网页的攻击，该网页试图获得对其他本地可访问文件的访问。

禁止从第三方主机加载内容。 这可能很难在应用程序内实现。 但是，开发人员可以覆盖shouldOverrideUrlLoading和shouldInterceptRequest来拦截，检查和验证从WebView中发起的大多数请求。 开发者还可以考虑通过使用URI类来检查URI的组件以确保其匹配已批准资源的列表中的条目来实现白名单方案。

示例代码 [https://gist.github.com/scottyab/6f51bbd82a0ffb08ac7a](https://gist.github.com/scottyab/6f51bbd82a0ffb08ac7a)

## 参考 

 * [http://labs.mwrinfosecurity.com/blog/2012/04/23/adventures-with-android-webviews/](http://labs.mwrinfosecurity.com/blog/2012/04/23/adventures-with-android-webviews/)
 * [https://developer.android.com/training/articles/security-tips.html#WebView](https://developer.android.com/training/articles/security-tips.html#WebView)
 
## CWE/OWASP

 * [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE-79: Improper Neutralization of Input During Web Page Generation (Cross-site Scripting)](http://cwe.mitre.org/data/definitions/79.html)
