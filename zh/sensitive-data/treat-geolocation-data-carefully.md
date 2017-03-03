# 谨慎处理地理位置数据

## 详细描述

Android和iOS可以使用GPS准确地确定位置。 处理此GPS数据是一个隐私问题，如果攻击者知道其当前或过去的位置，可能会使用户容易受到其他攻击。 本地蓝牙、NFC 、RFID标签的信息也可能泄漏地理位置信息。

此外，访问图库图片的应用程序也可以是用户的隐私问题，它可以通过检查时间戳并且假设图片是用户自己拍摄的图片来抓取存储在其中的GPS位置（如果有的话）。

## 建议

考虑使用和避免存储GPS数据的影响。 为了更好的隐私，尽量使用最粗粒度的位置服务。 除非必要，不要记录或存储GPS信息。 虽然在某些应用中使用GPS可能很有用，但很少需要记录和存储数据。 避免这种情况防止了许多隐私和安全问题。 GPS定位信息通常在iOS上的locationd缓存和Android上的各种缓存之间缓存一段时间。 一些应用程序自动使用GPS。 一个例子是通常对图像进行地理标记的相机。 如果这是一个问题，请确保从图像中剥离EXIF数据。

在需要安全的地点工作时，请记住，GPS数据可能会报告给Apple和Google服务器，以提高准确性。 Android和iOS设备都能捕获范围内附近接入点的信息，无论设备是否连接到它们。 不要在将在安全位置或其附近运行的应用程序中激活GPS，其坐标或无线网络拓扑不应报告给供应商。 除此之外，攻击者可以使用单个接入点的硬件地址的知识来模拟安全无线环境并从苹果或Google返回环境的GPS坐标。

## 参考

 * [http://www.sans.org/reading-room/whitepapers/forensics/forensic-analysis-ios-devices-34092](http://www.sans.org/reading-room/whitepapers/forensics/forensic-analysis-ios-devices-34092)

## CWE/OWASP 

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200](http://cwe.mitre.org/data/definitions/200.html)
