# Avoid Caching HTTP(S) Requests/Responses

## Details

By default, iOS’s `NSURLRequest` will cache responses in the Cache.db file. To prevent this insecure behavior, a developer must explicitly disable caching.

## Remediation

The developer can set the `cachePolicy` property of the `NSURLRequest` to disable the caching of HTTP(S) requests and responses. One of many methods for disabling caching is shown in the following code snippet (from [NSURLConnection Delegate Returns Null](http://stackoverflow.com/questions/30667340/nsurlconnection-delegate-returns-null) on Stack Overflow - http://stackoverflow.com/questions/30667340/nsurlconnection-delegate-returns-null):

`    (NSCachedURLResponse)connection:(NSURLConnection)connection
            willCacheResponse:(NSCachedURLResponse *)cachedResponse {
        return nil;`

Developers can find additional methods for disabling the caching of HTTP(S) requests and responses in the Apple Developer article “Understanding Cache Access” referenced below.

## References

 * [Understanding cache access](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/URLLoadingSystem/Concepts/CachePolicies.html) - https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/URLLoadingSystem/Concepts/CachePolicies.html

## CWE/OWASP

 * [M2 - Insecure Data Storage](https://www.owasp.org/index.php/Mobile_Top_10_2016-M2-Insecure_Data_Storage)
 * CWE: [CWE-312 - Cleartext Storage of Sensitive Information](http://cwe.mitre.org/data/definitions/312.html), [CWE-313 - Cleartext Storage in a File or on Disk](http://cwe.mitre.org/data/definitions/313.html), [CWE-522 - Insufficiently Protected Credentials](http://cwe.mitre.org/data/definitions/522.html)
