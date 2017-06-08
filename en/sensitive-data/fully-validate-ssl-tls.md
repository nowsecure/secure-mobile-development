# 3.3 Fully Validate SSL/TLS

Many apps do not properly validate SSL/TLS certificates, leaving them vulnerable to man-in-the-middle (MITM) attacks. If an app fails to properly validate its connection to the server, the app is susceptible to an MITM attack by a privileged network attacker. This type of attack gives the culprit the ability to capture, view, and modify traffic sent and received between the app and the server.

## Details

An application not properly validating its connection to the server is susceptible to a man-in-the-middle attack by a privileged network attacker.  This means that an attacker would be able to capture, view, and modify traffic sent and received between the application and the server.

### Common Mistake: Accepting self-signed certificates

Developers may disable certificate validation in apps for a variety of reasons. One example is when a developer needs to test code on the production server, but does not have a domain certificate for the test environment. In this situation, the developer may add code to the networking library to accept all certificates as valid. Accepting all certificates as valid, however, allows an attacker to execute an MITM attack on the app by simply using a self-signed certificate. This approach to developing an app nullifies the effect of SSL/TLS and provides no value over an unencrypted, plaintext connection (other than requiring an active MITM attack to view and modify traffic whereas a plaintext connection can be monitored passively).

Below is an example of vulnerable Android code that accepts all SSL/TLS certificates as valid:

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

### Common Mistake: Setting a permissive hostname verifier

Another common developer mistake in the implementation of SSL/TLS is setting a permissive hostname verifier. In this case, the app won’t accept self-signed certificates because the certificate is still validated. But if an app “allows all hostnames,” a certificate issued by any valid certificate authority (CA) for any domain name can be used to execute an MITM attack and sign traffic.

Below is an example of vulnerable Android code that sets a permissive hostname verifier:

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

## Remediation

### General guidance

For any app that handles highly sensitive data, use certificate pinning to protect against MITM attacks. The majority of apps have defined locations to which they connect (their backend servers) and inherently trust the infrastructure to which they connect, therefore it’s acceptable (and often more secure) to use a “private” public-key infrastructure, separate from public certificate authorities. With this approach, an attacker needs the private keys from the server side to perform a MITM attack against a device for which they do not have physical access.
If certificate pinning cannot be implemented for any app functionality that handles highly sensitive data, implement proper certificate validation, which consists of two parts:

1. **Certificate validation:** Certificates presented to the app must be fully validated by the app and be signed by a trusted root CA.
2. **Hostname validation:** The app must check and verify that the hostname (Common Name or CN) extracted from the certificate matches that of the host with which the app intends to communicate.

### For Android

Android 7.0 (API level 24) has introduced features that affect certificate pinning and validation. Android 7.0 will only trust a preselected list of certificate authorities (CAs) maintained by the Android Open Source Project and will not trust custom CAs or CAs added by a user.

Developers can, however, direct Android 7.0 to maintain trust with a custom CA throughout the entire app or specific domains using the Network Security Configuration file. Developers can also use the Network Security Configuration file for certificate pinning (see [Android documentation about the Network Security Configuration](https://developer.android.com/training/articles/security-config.html) feature.

Pinning certificates to a default Apache HTTP client shipped with Android consists of obtaining a certificate for the desired host, transforming the cert in .bks format, then pinning the cert to an instance of `DefaultHttpClient`. BKS keystores are usually included within the assets/raw directory of the app’s APK file.

The following sample code demonstrates how a BKS keystore can be loaded:

`    InputStream in = resources.openRawResource(certificateRawResource);

    keyStore = KeyStore.getInstance("BKS");
    keyStore.load(resourceStream, password);`

The constructed httpClient instance can be configured to only allow requests to host that present certificates that have been signed with certificates stored inside the application.

The following sample code illustrates this approach:
`    HttpParams httpParams = new BasicHttpParams();

    SchemeRegistry schemeRegistry = new SchemeRegistry();
    schemeRegistry.register(new Scheme("https", new SSLSocketFactory(keyStore), 443));

    ThreadSafeClientConnManager clientMan = new ThreadSafeClientConnManager(httpParams, schemeRegistry);

    httpClient = new DefaultHttpClient(clientMan, httpParams);`

For more information on implementing certificate pinning in Android, refer to the OWASP [Certificate and Public Key Pinning guide](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#Android) -  https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#Android.

In addition, [CWAC-NetSecurity](https://github.com/commonsguy/cwac-netsecurity) is a library that backports the Android 7.0 network security configuration subsystem going back to API level 17 (Android 4.2), which makes it easier to tie an app to particular certificate authorities or certificates, support self-signed certificates, and handle other advanced SSL certificate scenarios.

### For iOS
One option is to use `NSURLSession` or `AFNetworking` classes to achieve certificate pinning in iOS. Additional details on this implementation can be found in the technical note “[HTTPS Server Trust Evaluation](https://developer.apple.com/library/ios/technotes/tn2232/_index.html)” at https://developer.apple.com/library/ios/technotes/tn2232/_index.html.

In addition, [TrustKit](https://github.com/datatheorem/TrustKit), an open-source framework, can help make it easier for developers to deploy public key-pinning in iOS.


## References

* [Your app shouldn’t suffer SSL’s problems](https://moxie.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/) - https://moxie.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/

## CWE/OWASP

 * OWASP: [M3 - Insecure Communication](https://www.owasp.org/index.php/Mobile_Top_10_2016-M3-Insecure_Communication)
 * CWE: [CWE-319 - Cleartext Transmission of Sensitive Information](http://cwe.mitre.org/data/definitions/319.html)
