# 签名 Android APKs

## 详细描述 

APK应使用未过期的证书正确签名。

## 建议

- 使用生产证书（而不是调试证书）签署生产应用程序
- 确保证书包含足够的有效期（即，不会在应用的预期有效期内过期）
- Google建议您的证书至少使用2048位加密
- 确保包含签名密钥的密钥库被正确保护
- 此外，将密钥库的访问权限限制为只有那些绝对需要它的人

下面是一个生成私钥的Keytool命令的示例：

```
$ keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 10000
```

## 参考

 * [https://developer.android.com/tools/publishing/app-signing.html#cert](https://developer.android.com/tools/publishing/app-signing.html#cert)

## CWE/OWASP

 * [M6 - Broken Cryptography](https://www.owasp.org/index.php/Mobile_Top_10_2014-M6)
 * [CWE-310: Cryptographic Issues](http://cwe.mitre.org/data/definitions/310.html)
 * [CWE-326: Inadequate Encryption Strength](http://cwe.mitre.org/data/definitions/326.html)
 
 
