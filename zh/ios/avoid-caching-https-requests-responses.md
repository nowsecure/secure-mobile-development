# 避免缓存HTTP（S）请求/响应

## 详细描述 

默认情况下，iOS的`NSURLRequest`将响应缓存在Cache.db文件中。 为了防止这种不安全的行为，开发人员必须明确禁用缓存。

## 建议

开发人员可以设置`NSURLRequest`的`cachePolicy`属性来禁用HTTP（S）请求和响应的缓存。 禁用缓存的许多方法之一如下面的代码片段所示 (从Stack Overflow转载 [NSURLConnection Delegate Returns Null](http://stackoverflow.com/questions/30667340/nsurlconnection-delegate-returns-null) :

```   
 (NSCachedURLResponse)connection:(NSURLConnection)connection
            willCacheResponse:(NSCachedURLResponse *)cachedResponse {
        return nil;
        }
```

开发人员还可以在下面引用的Apple Developer文章“Understanding cache access”中找到禁用缓存HTTP（S）请求和响应的其他方法。

## 参考

 * [Understanding cache access](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/URLLoadingSystem/Concepts/CachePolicies.html) - https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/URLLoadingSystem/Concepts/CachePolicies.html
 
## CWE/OWASP 

 * OWASP Mobile Top 10: [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M2), [M4 - Unintended Data Leakage](https://www.owasp.org/index.php/Mobile_Top_10_2014-M4)
 * CWE: [CWE-312 - Cleartext Storage of Sensitive Information](http://cwe.mitre.org/data/definitions/312.html), [CWE-313 - Cleartext Storage in a File or on Disk](http://cwe.mitre.org/data/definitions/313.html), [CWE-522 - Insufficiently Protected Credentials](http://cwe.mitre.org/data/definitions/522.html)
 
