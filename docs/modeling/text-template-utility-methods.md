---
title: 文本模板实用工具方法
description: 了解在编辑器中编写代码时可用的各种文本模板实用工具Visual Studio。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663864"
---
# <a name="text-template-utility-methods"></a>文本模板实用工具方法

在文本模板中编写代码时，始终可以使用Visual Studio方法。 这些方法在 中定义 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> 。

> [!TIP]
> 还可以在未预处理文本模板的常规 (主机环境提供的其他) 和服务。 例如，可以解决文件路径、日志错误，并获取由 Visual Studio加载的包提供的服务。 有关详细信息，请参阅[从文本Visual Studio访问数据](/previous-versions/visualstudio/visual-studio-2010/gg604090\(v\=vs.100\))。

## <a name="write-methods"></a>写入方法

可以使用 和 `Write()` `WriteLine()` 方法在标准代码块内追加文本，而不是使用表达式代码块。 以下两个代码块在功能上是等效的。

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

### <a name="code-block-using-writeline"></a>使用 WriteLine 代码块 () 

```
<#
    int i = 10;
    while (i-- > 0)
    {
        WriteLine((i.ToString()));
    }
#>
```

你可能会发现，使用这些实用工具方法之一，而不是在具有嵌套控件结构的长代码块内使用表达式块会很有帮助。

和 方法具有两个重载，一个重载采用单个字符串参数，另一个重载采用复合格式字符串以及要包括在字符串中的对象数组 (`Write()` `WriteLine()` 如 `Console.WriteLine()` 方法) 。 的以下两个 `WriteLine()` 用法在功能上是等效的：

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

可以使用缩进方法设置文本模板的输出格式。 类 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> 具有一个字符串属性，该属性显示文本模板中的当前缩进，以及一个字段，该字段是已添加的缩进 `CurrentIndent` `indentLengths` 的列表。 可以使用 方法添加缩进，然后 `PushIndent()` 用 方法减去缩 `PopIndent()` 进。 如果要删除所有缩进，请使用 `ClearIndent()` 方法。 以下代码块演示如何使用这些方法：

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

此代码块生成以下输出：

```
Hello
        Hello
                Hello
Hello
        Hello
```

## <a name="error-and-warning-methods"></a>错误和警告方法

可以使用错误和警告实用工具方法将消息添加到错误Visual Studio列表中。 例如，以下代码将错误消息添加到错误列表。

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

## <a name="access-to-host-and-service-provider"></a>访问主机和服务提供商

属性 `this.Host` 可以提供对执行模板的主机公开的属性的访问权限。 若要使用 `this.Host` ，必须在 `hostspecific` 指令中设置 `<@template#>` 属性：

`<#@template ... hostspecific="true" #>`

的类型 `this.Host` 取决于执行模板的主机类型。 在 Visual Studio 中运行的模板中，可以将 强制转换到 ，以获得对服务（如 `this.Host` `IServiceProvider` IDE）的访问权限。 例如：

```
EnvDTE.DTE dte = (EnvDTE.DTE) ((IServiceProvider) this.Host)
                       .GetService(typeof(EnvDTE.DTE));
```

## <a name="using-a-different-set-of-utility-methods"></a>使用一组不同的实用工具方法

作为文本生成过程的一部分，模板文件将转换为类，该类始终命名为 `GeneratedTextTransformation` ，并且继承自 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> 。 如果要改为使用一组不同的方法，可以编写自己的类，在模板指令中指定它。 类必须从 继承 <xref:Microsoft.VisualStudio.TextTemplating.TextTransformation> 。

```
<#@ template inherits="MyUtilityClass" #>
```

使用 `assembly` 指令引用可在其中找到已编译类的程序集。
