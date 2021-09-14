---
title: T4 程序集指令
description: 了解在Visual Studio文本模板中，程序集指令加载程序集，以便模板代码可以使用其类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 5b376d71a23469f551be6230b7d9f16eb4637da8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663885"
---
# <a name="t4-assembly-directive"></a>T4 程序集指令

在Visual Studio时文本模板中， 指令加载程序集，以便 `assembly` 模板代码可以使用其类型。 效果类似于在项目中添加程序集Visual Studio引用。

 有关编写文本模板的一般概述，请参阅 [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

> [!NOTE]
> 运行时（预处理）文本模板中不需要 `assembly` 指令。 相反，将所需的程序集添加到 **项目Visual Studio引用**。

## <a name="using-the-assembly-directive"></a>使用 Assembly 指令
 该指令的语法如下所示：

```
<#@ assembly name="[assembly strong name|assembly file name]" #>
```

 程序集名称应为以下各项之一：

- GAC 中程序集的强名称，例如 `System.Xml.dll`。 还可以使用长形式，例如 `name="System.Xml, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"`。 有关详细信息，请参阅 <xref:System.Reflection.AssemblyName>。

- 程序集的绝对路径

  可以使用 语法 `$(variableName)` 来引用 Visual Studio变量（如 ）和 `$(SolutionDir)` `%VariableName%` 引用环境变量。 例如：

```
<#@ assembly name="$(SolutionDir)\MyProject\bin\Debug\SomeLibrary.Dll" #>
```

 在预处理文本模板中，assembly 指令无效。 请改为在项目的引用 **部分** 包含Visual Studio引用。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

## <a name="standard-assemblies"></a>标准程序集
 将自动加载以下程序集，您无需为它们编写程序集指令：

- `Microsoft.VisualStudio.TextTemplating.1*.dll`

- `System.dll`

- `WindowsBase.dll`

  如果您使用自定义指令，则指令处理器可能会加载其他程序集。 例如，如果您为域特定语言 (DSL) 编写模板，则无需为以下程序集编写程序集指令：

- `Microsoft.VisualStudio.Modeling.Sdk.1*.dll`

- `Microsoft.VisualStudio.Modeling.Sdk.Diagrams.1*.dsl`

- `Microsoft.VisualStudio.TextTemplating.Modeling.1*.dll`

- 包含 DSL 的程序集。

## <a name="using-project-properties-in-both-msbuild-and-visual-studio"></a><a name="msbuild"></a>在 MSBuild 和 Visual Studio
 Visual Studio $ (SolutionDir) 等宏在 MSBuild 中MSBuild。 如果你想要在生成计算机中转换模板，则必须改用项目属性。

 编辑 .csproj 或 .vbproj 文件以定义项目属性。 此示例定义一个名为 `myLibFolder` 的属性：

```xml
<!-- Define a project property, myLibFolder: -->
<PropertyGroup>
    <myLibFolder>$(MSBuildProjectDirectory)\..\libs</myLibFolder>
</PropertyGroup>

<!-- Tell the MSBuild T4 task to make the property available: -->
<ItemGroup>
    <T4ParameterValues Include="myLibFolder">
      <Value>$(myLibFolder)</Value>
    </T4ParameterValues>
  </ItemGroup>
```

 现在你可在文本模板中使用项目属性，此类模板将在 Visual Studio 和 MSBuild 中正确转换：

```
<#@ assembly name="$(myLibFolder)\MyLib.dll" #>
```

## <a name="see-also"></a>另请参阅

- [T4 包含指令](../modeling/t4-include-directive.md)
