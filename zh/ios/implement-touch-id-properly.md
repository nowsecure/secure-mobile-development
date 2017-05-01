# 正确应用Touch ID

## 详细描述 

Touch ID通常被用来允许用户在不输入密码的情况下对其设备进行认证和解锁。 一些开发人员还使用Touch ID，允许用户使用存储的设备指纹对其应用进行身份验证。

当开发人员在其应用中应用Touch ID时，通常会采用以下两种方式之一：

1. 仅使用本地认证框架来认证用户
  1. 这种方法使认证机制很容易被绕过
  2. 攻击者可以在运行时修改本地检查，或者通过修补二进制。 这可以通过覆盖`LAContextevaluatePolicy：localizedReason：reply`方法来实现
2. 使用钥匙串访问控制列表（ACL）

## 建议

当使用Touch ID进行身份验证时，将应用程序的密钥存储在钥匙串中，并将ACL分配给该项目。 使用此方法，iOS将在读取和将Keychain项目返回到应用程序之前执行用户存在检查。 开发人员可以在Apple网站上找到示例代码： [https://developer.apple.com/library/ios/samplecode/KeychainTouchID/Listings/KeychainTouchID_AAPLKeychainTestsViewController_m.html](https://developer.apple.com/library/ios/samplecode/KeychainTouchID/Listings/KeychainTouchID_AAPLKeychainTestsViewController_m.html).

## 参考

 * [KeychainTouchID: Using Touch ID with Keychain and LocalAuthentication](https://developer.apple.com/library/content/samplecode/KeychainTouchID/Introduction/Intro.html) - https://developer.apple.com/library/content/samplecode/KeychainTouchID/Introduction/Intro.html
 
## CWE/OWASP 

 * OWASP Mobile Top 10: [M5 - Poor Authorization and Authentication](https://www.owasp.org/index.php/Mobile_Top_10_2014-M5)
 * CWE: [CWE-288 - Authentication Bypass Using an Alternate Path or Channel](http://cwe.mitre.org/data/definitions/288.html)
