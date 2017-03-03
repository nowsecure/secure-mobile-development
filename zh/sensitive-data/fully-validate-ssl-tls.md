# 完全验证SSL / TLS

许多应用程序没有正确验证SSL / TLS证书，使他们容易受到中间人（MITM）攻击。 如果应用程序无法正确验证其与服务器的连接，则该应用程序容易受到特权网络攻击者的MITM攻击。 这种类型的攻击使罪犯能够捕获，查看和修改在应用程序和服务器之间发送和接收的流量。

## 详细描述

未正确验证其与服务器的连接的应用程序容易受到拥有网络管理权限的攻击者的中间人攻击。 这意味着攻击者将能够捕获，查看和修改在应用程序和服务器之间发送和接收的流量。

### 常见错误：接受自签名证书

开发人员可能会因为各种原因而停用应用中的证书验证。 一个例子是开发人员需要在生产服务器上测试代码，但没有测试环境的域证书。 在这种情况下，开发人员可以向网络库添加代码以接受所有有效的证书。 然而，接受所有证书为有效的，允许攻击者通过简单地使用自签名证书对应用程序执行MITM攻击。 这种开发应用程序的方法使SSL / TLS的效果无效，并且相对于未加密的纯文本连接（除了需要主动MITM攻击来查看和修改流量，而纯文本连接可以被动监控之外）没有实质上的安全提升。

以下是接受所有SSL / TLS证书的有效Android代码示例：

```java
    TrustManager[] trustAllCerts = new TrustManager[] {
       new X509TrustManager() {
          public java.security.cert.X509Certificate[] getAcceptedIssuers() {
            return null;
          }
          public void checkClientTrusted(X509Certificate[] certs, String authType) {  }

          public void checkServerTrusted(X509Certificate[] certs, String authType) {  }

       }
    };

    //Globally set the broken TrustManager
    SSLContext sc = SSLContext.getInstance("SSL");
    sc.init(null, trustAllCerts, new java.security.SecureRandom());
    HttpsURLConnection.setDefaultSSLSocketFactory(sc.getSocketFactory());

    //Make the connection to the server
    URL url = new URL("https://paypal.com");
    HttpsURLConnection urlConnection = (HttpsURLConnection) url.openConnection();
    InputStream ins = urlConnection.getInputStream();
    InputStreamReader isr = new InputStreamReader(ins);
    BufferedReader in = new BufferedReader(isr);

    String inputLine;
    in.close();
```

### 常见错误：设置允许的主机名验证器

在实施SSL / TLS时，另一个常见的开发人员错误是设置一个允许所有主机名的主机名验证器（hostname verifier）。 在这种情况下，应用程序将不接受自签名证书，证书仍然需要被验证。 但是如果应用程序“允许所有主机名”，任何有效的证书颁发机构（CA）为任何域名颁发的证书都可以被用来进行中间人攻击（MITM）和签名网络数据。

下面是一个易受攻击的Android代码示例，它设置了一个允许所有主机名的主机名验证器：

```java
    URL url = new URL("https://paypal.com");
    HttpsURLConnection urlConnection = (HttpsURLConnection) url.openConnection();
    urlConnection.setHostnameVerifier(SSLSocketFactory.ALLOW_ALL_HOSTNAME_VERIFIER);
    InputStream ins = urlConnection.getInputStream();
    InputStreamReader isr = new InputStreamReader(ins);
    BufferedReader in = new BufferedReader(isr);

    String inputLine;
    in.close();
```

## 建议

### 一般建议

对于处理高度敏感数据的任何应用程序，请使用证书锁定以防止MITM攻击。 大多数应用程序都定义了它们连接的位置（它们的后端服务器），并固有地信任它们连接的基础设施，因此使用“私有”公钥基础结构（与公共证书分开）是可以接受的（通常更安全） 当局。 使用这种方法，攻击者需要来自服务器端的私钥对他们没有物理访问的设备执行MITM攻击。

如果无法对处理高度敏感数据的任何应用程序功能实施证书锁定，请实施正确的证书验证，该证书验证由两部分组成：

1. **Certificate validation:** 呈现给应用程序的证书必须由应用程序完全验证，并由受信任的根CA进行签名。 
2. **Hostname validation:** 应用程序必须检查并验证从证书提取的主机名（公用名或CN）与应用程序要与之通信的主机的主机名相匹配。

### Android 建议

将证书固定到Android随附的默认Apache HTTP客户端包括获取所需主机的证书，转换.bks格式的证书，然后将证书固定到DefaultHttpClient实例。 BKS密钥库通常包含在应用程序的APK文件的assets / raw目录中。

以下示例代码演示了如何加载BKS密钥库：

```java
    InputStream in = resources.openRawResource(certificateRawResource);

    keyStore = KeyStore.getInstance("BKS");
    keyStore.load(resourceStream, password);
```

httpClient实例可以被配置为仅允许接受存在于应用程序内存储的证书签名的证书。

以下示例代码说明了此方法：

```    
	HttpParams httpParams = new BasicHttpParams();

    SchemeRegistry schemeRegistry = new SchemeRegistry();
    schemeRegistry.register(new Scheme("https", new SSLSocketFactory(keyStore), 443));

    ThreadSafeClientConnManager clientMan = new ThreadSafeClientConnManager(httpParams, schemeRegistry);

    httpClient = new DefaultHttpClient(clientMan, httpParams);
    
```

有关在Android中实现证书锁定的更多信息，请参阅OWASP [Certificate and Public Key Pinning guide](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#Android) 

此外，[CWAC-NetSecurity](https://github.com/commonsguy/cwac-netsecurity) 是一个将Android 7.0网络安全配置子系统返回到API级别17（Android 4.2）的库。它使得将应用程序绑定到特定的证书颁发机构或证书更容易。支持自签名证书，以及处理其他高级SSL证书方案。

### For iOS
一个方案是使用`NSURLSession`或`AFNetworking`类在iOS中实现证书锁定。 此实现的其他详细信息可以在apple developer网站上[HTTPS Server Trust Evaluation](https://developer.apple.com/library/ios/technotes/tn2232/_index.html)中找到。 

此外，一个开源框架的[TrustKit](https://github.com/datatheorem/TrustKit)可以帮助开发人员更容易地在iOS中部署公钥锁定。

## 参考

* [Your app shouldn’t suffer SSL’s problems](https://moxie.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/) - https://moxie.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/ 

## CWE/OWASP

 * OWASP Mobile Top 10: [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * CWE: [CWE-319 - Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
