---
layout: guide
title: "Fully validate SSL/TLS"
description: "Many apps do not properly validate SSL certificates, leaving them susceptible to man-in-the-middle attacks."
published: 1
categories:
  - handling-sensitive-data
series:
  name: Handling Sensitive Data
  index: 5
order: 203
---

## Details

An application not properly validating its connection to the server is susceptible to a man-in-the-middle attack by a priviledged network attacker.  This means that an attacker would be able to capture, view, and modify traffic sent and received between the application and the server.

## Accepting of self-signed certificates

It is common for developers to disable certificate validation in applications for many purposes.  For example, the developer may not way to test code on the production server, but does not have a domain/certificate for the test environment.  In this case, the developer may add some code to the networking library which allows all certificates to be valid.  By doing this, it allows an attacker to man-in-the-middle the application simply by using a self-signed certificate.  This effectively nullifies the value of TLS.  The only value this would gain you over a plaintext connection is the fact that it requires an active mitm to view/modify traffic.  Where as a plaintext connection can be passively mmonitored.

### Vulnerable code:
An example of the developer mistake would look something like the following on Android:

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

## Allow All Hostname Fail

Another common developer mistake in the implementation of SSL is to set a permissive host name verifier.  In this case the SSL cert is still validated, so it will not accept self signed certificates.  However, if you have a certificate issued for blahblahblah.com from a valid CA installed on the phone, you can use this cert to mitm and sign traffic for any app that "allows all hostnames".

An example of the developer mistake would look something like the following on Android:

### Vulnerable code

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

The landscape of TLS is quite a bit different than that of the web in that the developer controls the certificate validation code client side. In many cases, it is not necessary to use certificates from a public certificate authority, as these were designed for systems where the client did not know whether the system it was connecting to was trusted. Since the majority of applications know exactly where they are connecting to (their backend servers), and inherently trust the infrastructure they are connecting to, it is acceptable (and often more secure) to use a “private” public key infrastructure, separate from public certificate authorities. This way, an attacker would require the private keys from the server side in order to perform a MITM attack or other such types of attacks.

## References

* Android - [http://www.thoughtcrime.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/](http://www.thoughtcrime.org/blog/authenticity-is-broken-in-ssl-but-your-app-ha/)

## CWE/OWASP

 * [M3- Insufficient Transport Layer Protection](https://www.owasp.org/index.php/Mobile_Top_10_2014-M3)
 * [CWE 319](http://cwe.mitre.org/data/definitions/319.html)
