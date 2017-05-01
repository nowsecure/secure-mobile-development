# 安全的删除数据

## 详细描述 

在Android上，调用file.delete（）将不会安全地擦除目标文件，并且只要它没有被覆盖，它可以从设备的物理图像刻出。 由于对NAND闪存的积极管理，擦除文件的传统方法通常不在移动设备上工作。

## 建议

在假设任何写入设备的数据都可以恢复的情况下操作。 在某些情况下，加密可能会增加额外的保护层。

对于大多数应用程序不推荐使用以下方法，但可能删除文件并用大文件覆盖所有可用空间（这将迫使NAND闪存擦除所有未分配的空间）。 这种技术的缺点包括耗尽NAND闪存，导致应用和整个设备响应缓慢，并显着的功耗。

尽可能避免在设备上存储敏感数据。 

加密存储在文件中的敏感数据，在删除之前重写文件的内容和同步可以帮助，但是如上所述，它们不是完全可靠的解决方案。

## 参考 

 * [General Purpose Cypto](https://developer.apple.com/library/mac/documentation/security/conceptual/cryptoservices/GeneralPurposeCrypto/GeneralPurposeCrypto.html)
 
## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE-312: Cleartext Storage of Sensitive Information](http://cwe.mitre.org/data/definitions/312.html)
 * [CWE-313: Cleartext Storage in a File or on Disk](http://cwe.mitre.org/data/definitions/313.html)
