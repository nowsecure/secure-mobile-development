# 谨慎管理调试日志

## 详细描述 

调试日志通常设计为用于检测和纠正应用程序中的缺陷。 这些日志可能泄漏敏感信息，这可能有助于攻击者创建更强大的攻击。

## 建议

开发人员应考虑调试日志在生产环境中可能出现的风险。 一般来说，我们建议他们在生产中禁用。

通常由应用程序用于输出调试消息的Android系统日志是存储在存储器中的几千字节的循环缓冲器。 在内核崩溃的情况下，还可以从文件系统恢复调试日志。 在设备重新启动时，它被清除，但在此之前，具有READ_LOGS权限的任何Android应用程序都可以查询日志。 在最新版本的Android中，日志文件已被更仔细地隔离，并且不需要请求系统级权限。

在Android中，还可以利用ProGuard或DexGuard完全删除发布版本中Log类的方法调用，从而取消对Log.d，Log.i，Log.v，Log.e方法的所有调用。

在 *proguard.cfg* 中，添加以下代码段：

```
> -assumenosideeffects class android.util.Log { 
		> public static *** d(...);
		> public static *** v(...);
		> public static *** i(...);
		> public static *** e(...);
> }
```

在iOS上禁用NSLog语句将删除可能被拦截的潜在敏感信息，因为额外的好处可能会稍微提高应用程序的性能。 例如，一种方法是在生产构建中定义NSLog：

```
> #define NSLog(s,...)

This macro effectively removes all NSLog statements and replaces it with empty text at compilation time.

> NSLog(@”Breakpoint here with data %@”,data.description);

becomes effectively a no-op.

>	;
```

## CWE/OWASP 

 * [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10); [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8)
 * [CWE 215](http://cwe.mitre.org/data/definitions/215.html)
