# XDiamond 的日志模块

我们在 XDiamond 里面提供了一些用于输出信息的工具。

默认情况下，这些工具会将信息和警告输出倒终端。当然，你也可以借助命令行工具的输出重定向功能，将它们输出到指定的文件。

使用这些工具前，你需要导入相应的头文件。

```C++
#include "XDiamond/src/XDiamond2D/Log/XLog.h"
```

你可以用如下代码输出信息、警告和错误。

```C++
XDiamond2D::Logln("This is a line of log.");
XDiamond2D::Warningln("This is a line of warning.");
XDiamond2D::Errorln("This is a line of error.");
```

你会得到如下格式的报错信息。

![](https://docs.gpu.pub/images/log.png)

此外，我们还提供了一个 `XError` 类。这个类在输出红色错误信息的同时，还会将错误所在地的文件名、函数名和行号打印出来。

如需使用这个类，先导入 `XError.h`：

```C++
#include "XDiamond/src/XDiamond2D/Log/XError.h"
```

然后这样使用它：

```C++
XDiamond2D::XError err("Network broke");
err.Panic(X_CONTEXT);
```

会打印出如下报错：

![](https://docs.gpu.pub/images/error.png)

其中，`X_CONTEXT` 是一个宏定义，用于抓取错误所在地的位置信息。这是固定写法，请不要尝试更改。

**注：** C++ 和 Java 不同，不能在运行期间动态地获取错误的位置，所以抓取错误位置实际上是编译期的行为。抓取到的文件路径可能包含你的 Windows 用户名，请注意保护隐私。并且在生产环境中这种报错基本上是无意义的，这样的报错代码应该在编译期被剔除。