# 保护针对缓冲区溢出的攻击

## 详细描述 

这个最佳实践涵盖了三个iOS代码实现，帮助开发人员减轻缓冲区溢出攻击他们的应用程序的风险：自动引用计数（ARC），地址空间布局随机化（ASLR）和堆栈崩溃保护。

### 自动引用计数（ARC）

自动引用计数（ARC）是一种内存管理系统，在编译时自动处理对象的引用计数，而不是将此任务留给开发人员。 此功能是与iOS 5一起引入的，但它可以反向运行到以前的版本，因为操作是在编译时执行的。

* 编译器将自动插入释放和保留调用，使开发人员的生活更轻松，并降低引入与对象的内存生命周期相关的漏洞的风险。
* 因为该过程在编译时发生，所以它不引入任何运行时开销，例如与垃圾收集器不同。 因此，切换到ARC没有明显的缺点。


### 地址空间布局随机化（ASLR）

ASLR（地址空间布局随机化）是iOS 4.3中引入的一种安全功能，它随机化应用在内存中的加载和维护。 ASLR对应用程序中使用的地址空间进行随机化，使得在没有首先导致应用程序崩溃的情况下执行恶意代码变得很困难。 它还使转储分配的应用程序的内存的过程变得复杂。 此测试检查应用程序二进制文件是否使用-PIE（位置无关可执行文件）标志进行编译。

### 堆栈崩溃保护

当应用程序使用堆栈崩溃保护编译时，已知的值或“canary”被放置在堆栈上直接在局部变量之前，以保护保存的基指针，保存的指令指针和函数参数。 在函数返回时检查"canary"的值，以查看它是否已被覆盖。 编译器使用启发式方法来智能地将堆栈崩溃保护应用于函数（通常是使用字符数组的函数）。

## 建议

**启用 ARC** - 在Xcode项目中启用ARC，或者使用Xcode中的重构工具将现有项目迁移到ARC。

**ASLR** - 编译支持PIE的应用程序。 当通过命令行使用选项`-PIE`（在iOS 4.3或更高版本）上编译时，可以启用PIE。

**堆栈崩溃保护** - 使用`-fstack-protector-all`编译器标志编译应用程序，以保护应用程序免受缓冲区溢出攻击。

## 参考

  * [Transitioning to ARC Release Notes](https://developer.apple.com/library/content/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html) - https://developer.apple.com/library/content/releasenotes/ObjectiveC/RN-TransitioningToARC/Introduction/Introduction.html

  * [Address Space Layout Randomization](https://developer.apple.com/library/prerelease/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/BufferOverflows.html#//apple_ref/doc/uid/TP40002577-SW22) - https://developer.apple.com/library/prerelease/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/BufferOverflows.html#//apple_ref/doc/uid/TP40002577-SW22

  * [Other Compiler Flags That Affect Security](https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/BufferOverflows.html#//apple_ref/doc/uid/TP40002577-SW26) - https://developer.apple.com/library/content/documentation/Security/Conceptual/SecureCodingGuide/Articles/BufferOverflows.html#//apple_ref/doc/uid/TP40002577-SW26 

## CWE/OWASP

  * OWASP Mobile Top 10: [M10 - Lack of Binary Protections](https://www.owasp.org/index.php/Mobile_Top_10_2014-M10)
  * CWE: [CWE-121 - Stack-based Buffer Overflow](https://cwe.mitre.org/data/definitions/121.html), [CWE-200 - Information Exposure](http://cwe.mitre.org/data/definitions/200.html)
  