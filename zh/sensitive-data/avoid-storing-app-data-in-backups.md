# 避免将应用程序数据存储在备份中

## 详细描述 

在Android或iOS设备上执行数据备份还可以备份存储在应用程序的私人目录中的敏感信息。

## 建议

### Android

默认情况下，Android应用程序的Manifest文件中的`allowBackup`的值为`true`。 这将产生一个Android备份文件（backup.ab），包括设备文件系统上的应用程序私有目录中包含的所有子目录和文件。 因此，显式声明`allowBackup`标志为`false`。

### iOS

在对安装了特定应用程序的设备执行iTunes备份时，备份将包括设备文件系统上包含在该应用程序的私人目录中的所有子目录（“Caches”子目录除外）和文件。 因此，请避免将任何敏感数据以明文存储在应用程序的私有目录或子目录中的任何文件或文件夹中（另请参见最佳做法3.1 [实现安全数据存储](implement-secure-data-storage.md)）。

## CWE/OWASP 

 * OWASP Mobile Top 10: [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2), [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * CWE: [CWE-538 - File and Directory Information Exposure](http://cwe.mitre.org/data/definitions/538.html)
 
