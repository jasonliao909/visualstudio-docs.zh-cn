---
title: 文本模板实用工具方法
description: 了解在 Visual Studio 中写入代码时可用的各种文本模板实用工具方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- text templates, utility methods
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 7ee6eff6c47a818eca29673b5aad6905e6f52e28
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663864"
---
# <a name="text-template-utility-methods"></a>文本模板实用工具方法

在 Visual Studio 文本模板中写入代码时，这几种方法始终可用。 在 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> 中定义这些方法。

> [!TIP]
> 还可以在常规（未预处理）文本模板中使用主机环境提供的其他方法和服务。 例如，可以解决文件路径、记录错误并获取 Visual Studio 和任意已加载包提供的服务。 有关详细信息，请参阅[从文本模板访问 Visual Studio](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\))。

## <a name="write-methods"></a>写入方法

可以使用 `Write()` 和 `WriteLine()` 方法在标准代码块内追加文本，而不是使用表达式代码块。 以下两个代码块功能一样。

### <a name="code-block-with-an-expression-block"></a>包含表达式块的代码块

```
<#
int i = 10;
while (i-- > 0)
    { #>
        <#= i #>
    <# }
#>
```

### <a name="code-block-using-writeline"></a>使用 WriteLine() 的代码块

```
<#
    int i = 10;
    while (i-- > 0)
    {
        WriteLine((i.ToString()));
    }
#>
```

你会发现使用其中一个这些实用工具方法（而不是长代码块中具有嵌套控件结构的表达式块）会很有帮助。

`Write()` 和 `WriteLine()` 方法具有两个加载，一个采用单个字符串参数，另一个采用组合格式字符串和要包含在字符串中的对象阵列（如 `Console.WriteLine()` 方法）。 `WriteLine()` 的以下两种用法功能一样：

```
<#
    string msg = "Say: {0}, {1}, {2}";
    string s1 = "hello";
    string s2 = "goodbye";
    string s3 = "farewell";

    WriteLine(msg, s1, s2, s3);
    WriteLine("Say: hello, goodbye, farewell");
#>
```

## <a name="indentation-methods"></a>缩进方法

可以使用缩进方法设置文本模板的输出格式。 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> 类具有 `CurrentIndent` 字符串属性，可以显示文本模板中的当前缩进，还具有 `indentLengths` 字段，其中包含已添加的缩进列表。 可以使用 `PushIndent()` 方法添加缩进，使用 `PopIndent()` 方法减去缩进。 如果要删除所有缩进，请使用 `ClearIndent()` 方法。 以下代码块演示这些方法的用法：

```
<#
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
    ClearIndent();
    WriteLine(CurrentIndent + "Hello");
    PushIndent("    ");
    WriteLine(CurrentIndent + "Hello");
#>
```

此代码生成以下输出：

```
Hello
        Hello
                Hello
Hello
        Hello
```

## <a name="error-and-warning-methods"></a>错误和警告方法

可以使用错误和警告实用工具方法将消息添加到 Visual Studio 错误列表中。 例如，以下代码将错误消息添加到错误列表。

```
<#
  try
  {
    string str = null;
    Write(str.Length.ToString());
  }
  catch (Exception e)
  {
    Error(e.Message);
  }
#>
```

## <a name="access-to-host-and-service-provider"></a>对主机和服务提供商的访问

属性 `this.Host` 可以提供对由正在执行模板的主机公开的属性的访问。 若要使用 `this.Host`，必须在 `<@template#>` 指令中设置 `hostspecific` 属性：

`<#@template ... hostspecific="true" #>`

`this.Host` 的类型取决于正在其中执行模板的主机类型。 在 Visual Studio 中运行的模板中，可以将 `this.Host` 强制转换为 `IServiceProvider`，以获取对服务（如 IDE）的访问。 例如：

```
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
```

## <a name="using-a-different-set-of-utility-methods"></a>使用一组不同的实用工具方法

作为文本生成过程的一部分，模板文件将转换为类，该类始终命名为 `GeneratedTextTransformation`，并且继承自 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation>。 如果要改为使用一组不同的方法，则可以编写自己的类，并在模板指令中指定它。 类必须从 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> 继承。

```
<#@ template inherits="MyUtilityClass" #>
```

使用 `assembly` 指令引用可在其中找到已编译类的程序集。
