# 避免存储缓存的摄像机图像

远程支票存款应用程序允许一个人用手机的相机拍摄支票的图片，然后将图像发送到他们的金融机构存入他们的帐户。

## 详细描述 

使用远程支票存款应用程序，一个人可以用手机的相机拍照支票，然后将图像发送到他们的金融机构存入他们的帐户。 许多这些应用程序将保留检查图像（或其一部分）在移动设备的NAND内存中，即使它被删除。

## 建议

不要在设备上使用非易失性存储器传输支票图像，支票图像可能会残留。 一个可能的替代方案是：

1. 创建一个SurfaceView，显示相机预览或实时预览相机传感器所看到的内容
2. 插入并编程一个按钮，当按下时，将相机预览作为像素阵列返回
3. 最后，将像素阵列转换为位图，将其压缩为.jpg，将其编码为Base64，并将其提交到远程位置

此方法将只维护易失性内存中的图像，并防止支票图像在非易失性存储器中的缓存。

特别是使用Android Camera类，可以使用方法takePicture指定当使用`Camera.PictureCallback`接口生成.jpg时的回调。 特别是，我们对方法“public void onPictureTaken（byte [] bytes，Camera camera）感兴趣。

使用这种技术，可以使用“bytes”数组内容，其中包含RAM中的照片。
 
## CWE/OWASP

 * [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * [CWE 200: Information Exposure](http://cwe.mitre.org/data/definitions/200.html)
