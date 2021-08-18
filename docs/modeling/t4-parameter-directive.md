---
title: T4 参数指令
description: 请注意，在 Visual Studio 中，参数指令声明模板代码中从外部上下文传入的值初始化的属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: a8a6101915112c1d7035611bec84c6c8d6bf6bc4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122085359"
---
# <a name="t4-parameter-directive"></a>T4 参数指令

在 Visual Studio 文本模板中， `parameter` 指令声明模板代码中从外部上下文传入的值初始化的属性。 如果编写调用文本转换的代码，则可以设置这些值。

## <a name="using-the-parameter-directive"></a>使用参数指令

```
<#@ parameter type="Full.TypeName" name="ParameterName" #>
```

 `parameter`指令声明模板代码中从外部上下文传入的值初始化的属性。 如果编写调用文本转换的代码，则可以设置这些值。 值可以在字典中传递 `Session` ，也可以在中传递 <xref:System.Runtime.Remoting.Messaging.CallContext> 。

 可声明任何可远程处理的类型的参数。 也就是说，该类型必须用进行声明 <xref:System.SerializableAttribute> ，或者必须派生自 <xref:System.MarshalByRefObject> 。 这允许将参数值传递到处理模板的 AppDomain。

 例如，你可以编写包含以下内容的文本模板：

```
<#@ template language="C#" #>

<#@ parameter type="System.Int32" name="TimesToRepeat" #>

<# for (int i = 0; i < TimesToRepeat; i++) { #>
Line <#= i #>
<# } #>
```

## <a name="passing-parameter-values-to-a-template"></a>将参数值传递给模板
 如果要编写 Visual Studio 扩展（如菜单命令或事件处理程序），则可以使用文本模板化服务来处理模板：

```csharp
// Get a service provider - how you do this depends on the context:
IServiceProvider serviceProvider = dte; // or dslDiagram.Store, for example
// Get the text template service:
ITextTemplating t4 = serviceProvider.GetService(typeof(STextTemplating)) as ITextTemplating;
ITextTemplatingSessionHost host = t4 as ITextTemplatingSessionHost;
// Create a Session in which to pass parameters:
host.Session = host.CreateSession();
// Add parameter values to the Session:
session["TimesToRepeat"] = 5;
// Process a text template:
string result = t4.ProcessTemplate("MyTemplateFile.t4",
  System.IO.File.ReadAllText("MyTemplateFile.t4"));
```

## <a name="passing-values-in-the-call-context"></a>在调用上下文中传递值
 您还可以在中将值作为逻辑数据传递 <xref:System.Runtime.Remoting.Messaging.CallContext> 。

 下面的示例通过使用这两种方法传递值：

```csharp
ITextTemplating t4 = this.Store.GetService(typeof(STextTemplating)) as ITextTemplating;
ITextTemplatingSessionHost host = t4 as ITextTemplatingSessionHost;
host.Session = host.CreateSession();
// Pass a value in Session:
host.Session["p1"] = 32;
// Pass another value in CallContext:
System.Runtime.Remoting.Messaging.CallContext.LogicalSetData("p2", "test");

// Process a small template inline:
string result = t4.ProcessTemplate("",
   "<#@parameter type=\"System.Int32\" name=\"p1\"#>"
 + "<#@parameter type=\"System.String\" name=\"p2\"#>"
 + "Test <#=p1#> <#=p2#>");

// Result value is:
//     Test 32 test
```

## <a name="passing-values-to-a-run-time-preprocessed-text-template"></a>将值传递给 Run-Time (预处理) 文本模板
 通常不需要在 `<#@parameter#>` 运行时 (预处理) 文本模板中使用指令。 相反，您可以为生成的代码定义其他构造函数或可设置的属性，通过这些构造函数传递参数值。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

 但是，如果要 `<#@parameter>` 在运行时模板中使用，则可以通过使用会话字典将值传递给它。 例如，假设已创建一个名为的预处理模板文件 `PreTextTemplate1` 。 你可以使用以下代码在你的程序中调用该模板。

```csharp
PreTextTemplate1 t = new PreTextTemplate1();
t.Session = new Microsoft.VisualStudio.TextTemplating.TextTemplatingSession();
t.Session["TimesToRepeat"] = 5;
// Add other parameter values to t.Session here.
t.Initialize(); // Must call this to transfer values.
string resultText = t.TransformText();
```

## <a name="obtaining-arguments-from-texttemplateexe"></a>从 TextTemplate.exe 获取参数

> [!IMPORTANT]
> `parameter`指令不检索在实用工具的参数中设置的值 `-a` `TextTransform.exe` 。 若要获取这些值，请 `hostSpecific="true"` 在 `template` 指令中设置并使用 `this.Host.ResolveParameterValue("","","argName")` 。
