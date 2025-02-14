---
title: T4 参数指令
description: 了解在 Visual Studio 中，参数指令如何在模板代码中声明属性，这些属性是从外部上下文传入的值初始化的。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663872"
---
# <a name="t4-parameter-directive"></a>T4 参数指令

在 Visual Studio 文本模板中，`parameter` 指令在模板代码中声明属性，这些属性是从外部上下文传入的值初始化的。 如果编写调用文本转换的代码，可以设置这些值。

## <a name="using-the-parameter-directive"></a>使用参数指令

```
<#@ parameter type="Full.TypeName" name="ParameterName" #>
```

 `parameter` 指令在模板代码中声明属性，这些属性是从外部上下文传入的值初始化的。 如果编写调用文本转换的代码，可以设置这些值。 这些值可以在 `Session` 字典中传递，也可以在 <xref:System.Runtime.Remoting.Messaging.CallContext> 中传递。

 可以声明任何可远程处理类型的参数。 也就是说，必须使用 <xref:System.SerializableAttribute> 声明该类型，或者它必须派生自 <xref:System.MarshalByRefObject>。 这允许将参数值传递到处理模板的 AppDomain 中。

 例如，可以编写包含以下内容的文本模板：

```
<#@ template language="C#" #>

<#@ parameter type="System.Int32" name="TimesToRepeat" #>

<# for (int i = 0; i < TimesToRepeat; i++) { #>
Line <#= i #>
<# } #>
```

## <a name="passing-parameter-values-to-a-template"></a>将参数值传递给模板
 如果要编写 Visual Studio 扩展（如菜单命令或事件处理程序），可以使用文本模板化服务处理模板：

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
 或者，可以在 <xref:System.Runtime.Remoting.Messaging.CallContext> 中将值作为逻辑数据传递。

 以下示例使用这两种方法传递值：

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

## <a name="passing-values-to-a-run-time-preprocessed-text-template"></a>将值传递给运行时间（预处理过）文本模板
 通常不需要将 `<#@parameter#>` 指令与运行时间（预处理过）文本模板一起使用。 相反，你可以为生成的代码定义附加的构造函数或可设置的属性，由此传递参数值。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

 但是，如果要在运行时间模板中使用 `<#@parameter>`，可以使用会话字典将值传递给该模板。 例如，假设你已创建该文件作为名为 `PreTextTemplate1` 的预处理模板。 可以使用以下代码在程序中调用模板。

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
> `parameter` 指令不检索在 `TextTransform.exe` 实用工具的 `-a` 参数中设置的值。 若要获取这些值，在 `template` 指令中设置 `hostSpecific="true"`，并使用 `this.Host.ResolveParameterValue("","","argName")`。
