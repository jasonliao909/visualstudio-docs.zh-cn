---
title: 从文本模板访问 Visual Studio 或其他主机
description: 了解如何在文本模板中使用由执行模板的主机公开的方法和属性。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 5a812279046bf1b2eb987719762098697ddd8eb1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664791"
---
# <a name="access-visual-studio-or-other-hosts-from-a-text-template"></a>从文本模板访问 Visual Studio 或其他主机

在文本模板中，可以使用由执行模板的主机公开的方法和属性。 Visual Studio 是主机的一个示例。

> [!NOTE]
> 你可以在常规文本模板中使用主机方法和属性，但不能在预处理文本模板中使用。

## <a name="obtain-access-to-the-host"></a>获取对主机的访问权限

若要访问主机，请在 `template` 指令中设置 `hostspecific="true"`。 现在，可以使用 `this.Host`，类型为 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110))。 [ITextTemplatingEngineHost](/previous-versions/visualstudio/visual-studio-2012/bb126505(v=vs.110)) 类型具有可用于解析例如文件名和日志错误的成员。

### <a name="resolve-file-names"></a>解析文件名

若要查找相对于文本模板的文件的完整路径，请使用 `this.Host.ResolvePath()`。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.IO" #>
<#
 // Find a path within the same project as the text template:
 string myFile = File.ReadAllText(this.Host.ResolvePath("MyFile.txt"));
#>
Content of myFile is:
<#= myFile #>
```

### <a name="display-error-messages"></a>显示错误消息

此示例在转换模板时记录消息。 如果主机是 Visual Studio，则错误将添加到“错误列表”。

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ import namespace="System.CodeDom.Compiler" #>
<#
  string message = "test message";
  this.Host.LogErrors(new CompilerErrorCollection()
    { new CompilerError(
       this.Host.TemplateFile, // Identify the source of the error.
       0, 0, "0",   // Line, column, error ID.
       message) }); // Message displayed in error window.
#>
```

## <a name="use-the-visual-studio-api"></a>使用 Visual Studio API

如果在 Visual Studio 中执行文本模板，可以使用 `this.Host` 访问 Visual Studio 提供的服务和加载的任何包或扩展。

设置 hostspecific="true" 并将 `this.Host` 强制转换为 <xref:System.IServiceProvider>。

此示例将 Visual Studio API <xref:EnvDTE.DTE> 作为服务：

```csharp
<#@ template hostspecific="true" language="C#" #>
<#@ output extension=".txt" #>
<#@ assembly name="EnvDTE" #>
<#@ import namespace="EnvDTE" #>
<#
 IServiceProvider serviceProvider = (IServiceProvider)this.Host;
 DTE dte = serviceProvider.GetService(typeof(DTE)) as DTE;
#>
Number of projects in this solution: <#=  dte.Solution.Projects.Count #>
```

## <a name="use-hostspecific-with-template-inheritance"></a>将 hostSpecific 与模板继承一同使用

如果你还使用 `inherits` 属性，并且如果从指定 `hostspecific="true"` 的模板继承，则指定 `hostspecific="trueFromBase"`。 如果没有，可能会收到编译器警告，指示属性 `Host` 已声明两次。
