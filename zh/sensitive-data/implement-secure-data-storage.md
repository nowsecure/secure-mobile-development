# 实现安全数据存储

## 详细信息 

在移动设备上安全地存储数据需要适当的技术。 只要有可能***“简单地不要存储或缓存数据”*** 是避免数据在设备上被获取最直接的方式。

## 建议

尽量不要存储敏感数据。 减少用户信息存储的方法包括：

* 仅仅传输和显示，但不持久化存储中。 这还需要特别注意防止敏感数据的屏幕截图被写入磁盘。
* 仅存储在内存中（在应用程序关闭时清除）。

### 附加分层加密
如果在设备上存储敏感数据是应用程序需求，则应向数据添加额外的经过验证的第三方加密（例如，[SQLCipher](https://www.zetetic.net/sqlcipher/)）。

通过添加另一层加密，您可以更好地控制实施和攻击，主要集中在主要的操作系统加密类。 例如，对iOS数据保护类（现在已被入侵）的攻击将无法直接危害您的应用程序。 这种方法具有更复杂的缺点，并且如果实施得不好，实际上会减少安全系数。 如果您不确定是否包括经过验证的第三方加密库，Apple和Android的通用加密库提供了许多标准加密功能，如果使用得当，可以提供相当安全的加密实现。

下面是一些方法：

 * 使用SQLCipher在SQLite数据库中加密敏感值，使用[PRAGMA key](https://www.zetetic.net/sqlcipher/sqlcipher-api/#key)加密整个数据库
 * PRAGMA key可以在用户初次安装应用程序或第一次启动时在运行时生成
 * 为每个用户和设备生成唯一的PRAGMA密钥
 * 密钥生成的源应当具有足够的熵（即，避免从诸如用户名的易于预测的数据生成密钥材料）

每当您加密用户数据时，旨在使用随机生成的主密钥对其进行加密，该主密钥在用户访问数据时也使用用户提供的密码加密。 这将防止数据被容易地恢复，如果攻击者从设备中提取主密钥。 由于Apple的数据保护API和钥匙串中的漏洞数量以及大多数Android手机上缺少设备加密，因此不建议将主密钥或密码存储在设备上。

### Android
在Android中，记住外部存储设备（如SD卡）没有细粒度的权限，任何应用程序默认情况下具有对存储的读访问权限，可以读取所有文件。 从Android 4.4开始应用程序可以在某些情况下以受保护的方式在SD卡上存储数据 (参考 [http://source.android.com/devices/tech/storage/](http://source.android.com/devices/tech/storage/)).

Android和iOS实现标准加密库，例如AES，可用于保护数据。 请注意被此方法加密的数据安全依赖于用于导出密钥和密钥管理的密码安全。 需要考虑密码策略，长度和复杂性与用户方便性以及加密密钥如何存储在内存中。 而且root权限可以转储正在运行的进程的内存，并搜索它的加密密钥。

还要注意，使用标准加密提供程序“AES”通常将默认为较不安全的AES-ECB。 最佳做法是使用256位密钥和SecureRandom生成的随机IV指定AES-CBC或AES-GCM。 您还应该使用经过良好测试的PBKDF2（基于密码的密钥导出函数）来从密码导出密钥。

### iOS

iOS中内置的数据保护API与复杂的密码短语相结合，可以提供额外的数据保护层，但不像实施其他第三方验证的加密技术那么安全。 为了利用这一点，文件必须被专门标记。(参考最佳实践 6.1 [谨慎使用keychain](/iOS/use-the-keychain-carefully)). 任何没有专门使用apple 的文件保护api加密的数据都是未加密存储的

## 参考

 * [Android/iOS Full Database Encryption](http://sqlcipher.net/) - http://sqlcipher.net/
 * [Android Storage Options](http://developer.android.com/guide/topics/data/data-storage.html) - http://developer.android.com/guide/topics/data/data-storage.html

## CWE/OWASP 

 * OWASP Mobile Top 10: [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2)
 * CWE: [CWE-312 - Cleartext Storage of Sensitive Information](http://cwe.mitre.org/data/definitions/312.html), [CWE-313 - Cleartext Storage in a File or on Disk](http://cwe.mitre.org/data/definitions/313.html), [CWE-522 - Insufficiently Protected Credentials](http://cwe.mitre.org/data/definitions/522.html), [CWE-215 - Information Exposure Through Debug Information](http://cwe.mitre.org/data/definitions/215.html)
