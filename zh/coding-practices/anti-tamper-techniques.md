# 实施防篡改技术

## 详细描述 

攻击者可以在应用上篡改或安装后门，重新签名并将恶意版本发布到第三方应用市场。 这种攻击通常针对流行的应用程序和金融应用程序。

## 建议

采用防篡改和篡改检测技术来防止非法应用程序执行。

使用校验和，数字签名和其他验证机制来帮助检测文件篡改。 当攻击者试图操纵应用程序时，不会保留正确的校验和，并且这可以检测和防止非法执行。 注意，这样的技术不是万无一失的，并且可以被充分动机的攻击者绕过。 校验和，数字签名和其他验证技术增加了攻击者必须花费的时间和精力才能成功地破坏应用程序。 应用程序可以在检测到篡改的情况下以静默方式擦除其用户数据，密钥或其他重要数据，以进一步挑战攻击者。 检测到篡改的应用程序还可以通知管理员。

在Android上，用于签名应用程序的公钥可以从应用程序的证书中读取，并用于验证应用程序是否已使用开发人员的私钥签名。 使用PackageManager类，可以检索应用程序的签名，然后将它们与正确的值进行比较。 如果有人篡改或重新签名了应用程序，比较将失败，导致检测到篡改应用程序。

## 参考 

 * Android - [https://gist.github.com/scottyab/b849701972d57cf9562e](https://gist.github.com/scottyab/b849701972d57cf9562e)
 
## CWE/OWASP

 * [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE-354: Improper Validation of Integrity Check Value](http://cwe.mitre.org/data/definitions/354.html)
