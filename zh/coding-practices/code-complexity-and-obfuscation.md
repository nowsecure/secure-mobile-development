# 增加代码复杂性和使用混淆

## 详细描述

反向工程应用程序可以提供有价值的洞察您的应用程序的工作原理。 使您的应用程序在内部更复杂，攻击者更难以看到应用程序如何操作，这可以减少攻击面的数量。

## 建议

反向工程一个Android应用程序（.apk文件）是很容易实现的，然后可以检查应用程序的内部工作。 混淆代码，以使恶意用户更难以检查应用程序的内部工作，如下面链接到Android开发人员参考文章中所述。

此外，由于iOS应用程序的设计方式，它们容易受到逆向工程攻击。 应用程序的类和协议存储在对象文件中，允许攻击者完全映射应用程序的设计。 Objective-C本身是一种反射语言，能够感知和修改自己的状态; 具有正确工具的攻击者可以以与运行时管理应用程序相同的方式感知和修改应用程序的状态。 Objective-C包含一个简单的消息框架，它非常容易跟踪，并且可以被操纵来拦截甚至篡改应用程序的运行时。 可以使用相对简单的攻击来操纵Objective-C运行时绕过身份验证和策略检查，内部应用程序健全检查或警告应用程序策略的那种逻辑检查。

如果应用程序处理高度敏感的数据，请考虑实施反调试技术。 存在可以增加逆向工程代码的复杂性的各种技术。 一种技术是使用C / C ++来限制攻击者轻松地运行操作。 有丰富的C和C ++库，它们非常成熟，并且易于与Objective-C集成，并且Android提供了JNI（Java Native Interface）。 在iOS上，考虑在低级C中编写代码的关键部分，以避免Objective-C运行时或Objective-C逆向工程工具（如class-dump，class-dump-z，Cycript或Frida）的暴露和操作。

**限制调试器 –** 应用程序可以使用特定的系统调用来指定，以防止操作系统允许调试器附加到进程。 通过防止调试器attach到进程，攻击者干扰低级运行时的能力受到限制。 攻击者必须首先规避调试限制，以便在低级别上攻击应用程序。 这增加了攻击的进一步复杂性。 Android应用程序应该在应用程序清单中设置“android：debuggable =”false“”，以防止攻击者或恶意软件轻松运行运行时操作。 在iOS上，您可以使用`PT_DENY_ATTACH`。

**跟踪检查 –** 应用程序可以确定其当前是否由调试器或其他调试工具跟踪。 如果正在被跟踪，则应用可以执行任何数量的响应动作，例如，丢弃加密密钥以保护用户数据，通知服务器管理员或其他这样的响应以试图保护自身。 可以通过检查进程状态标志或使用其他技术（例如比较“ptrace attach”的返回值，检查父进程，将进程列表中的调试器列入黑名单或比较程序不同部分的时间戳）来检测调试器跟踪。

**优化 -** 为了隐藏高级数学计算和其他类型的复杂逻辑，利用编译器优化可以帮助混淆目标代码，使其不容易被攻击者反汇编。 这使得攻击者更难以获得对特定代码的理解。 在Android中，通过使用本机编译库和本机开发工具包（NDK）可以更容易地实现。 此外，使用LLVM Obfuscator或任何保护程序SDK将提供更好的机器代码混淆。

**Stripping binaries –** 清除原生二进制文件是增加攻击者所需的时间和技能以便查看应用程序低级功能的有效方法。 通过剥离二进制，二进制的符号表被剥离，以便攻击者不能轻易地调试或反向工程应用程序。 剥离二进制文件不会丢弃iOS上的Objective-C类或对象映射数据。 在Android上，您可以重用在gNU / Linux系统上使用的技术，例如`sstrip`或使用UPX。

分布在App Store中的iOS应用程序中的二进制文件被加密，增加了另一层的复杂性。 虽然存在从这些二进制文件中剥离FairPlay数字版权管理（DRM）加密的工具，但这一层DRM增加了攻击二进制所需的时间和熟练程度。 然而，App Store应用程序中使用的加密可能会被熟练的攻击者剥离。 攻击者通过转储在运行时从设备的内存中直接加载应用程序的内存来实现这一点。

## 参考

### Android
 * [ProGuard](http://proguard.sourceforge.net/) and <http://developer.android.com/tools/help/proguard.html>
 * [DexGuard](http://www.saikoa.com/dexguard)
 * [DashO](https://www.preemptive.com/products/dasho/overview)

### iOS
 * [PreEmptive Protection for iOS - Rename](https://github.com/preemptive/PPiOS-Rename)
 * [ObjC-Obfuscator](https://github.com/FutureWorkshops/Objc-Obfuscator)
 * [FairPlay DRM overview](https://www.theiphonewiki.com/wiki/Copy_Protection_Overview)
 * [Bugging Debuggers](https://www.theiphonewiki.com/wiki/Bugging_Debuggers)
 * [PreEmptive Protection for iOS - ControlFlow](https://www.preemptive.com/products/ppios)

### Other / Multi
 * [LLVM-Obfuscator](https://github.com/obfuscator-llvm/obfuscator/wiki) (iOS, Android, others)
 * [Dotfuscator Community Edition](https://www.preemptive.com/products/dotfuscator/compare-editions) (.NET Obfuscator with Xamarin support)

## CWE/OWASP

 * [OWASP Mobile Application Security Verification Standard, Resiliency Against Reverse Engineering Requirements](https://github.com/OWASP/owasp-masvs/blob/master/Document/0x15-V9-Resiliency_Against_Reverse_Engineering_Requirements.md)
 * [M8 - Security Decisions via Untrusted Inputs](https://www.owasp.org/index.php/Mobile_Top_10_2014-M8); [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
 * [CWE-656: Reliance on Security Through Obscurity](http://cwe.mitre.org/data/definitions/656.html)

