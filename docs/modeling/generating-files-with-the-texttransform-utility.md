---
title: 使用 TextTransform 实用工具生成文件
description: 了解 TextTransform 实用工具如何成为一个可用于转换文本模板的命令行工具。
ms.custom: SEO-VS-2020
ms.date: 07/26/2019
ms.topic: conceptual
helpviewer_keywords:
- text templates, TextTransform utility
- TextTransform.exe
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 82a0a5ec91b532e96c795ad65910061b0d5f946e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664171"
---
# <a name="generate-files-with-the-texttransform-utility"></a>使用 TextTransform 实用工具生成文件

TextTransform.exe 是一个可用于转换文本模板的命令行工具。 调用 TextTransform.exe 时，指定文件模板文件的名称作为参数。 TextTransform.exe 调用文本转换引擎，并处理文本模板。 TextTransform.exe 通常从脚本调用。 但是，通常不需要这样做，因为可以在 Visual Studio 中或在生成过程中执行文本转换。

> [!NOTE]
> 如果要在生成过程中执行文本转换，请考虑使用 MSBuild 文本转换任务。 有关详细信息，请参阅[生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)。 在安装了 Visual Studio 的计算机上，还可以编写可以转换文本模板的应用程序或 Visual Studio 扩展。 有关详细信息，请参阅[使用自定义主机处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)。

TextTransform.exe 位于以下目录中：

::: moniker range=">=vs-2019"

\Program Files (x86)\Microsoft Visual Studio\2019\Professional\Common7\IDE

适用于 Professional 版或

\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE

适用于 Enterprise 版。

::: moniker-end

::: moniker range="vs-2017"

\Program Files (x86)\Microsoft Visual Studio\2017\Professional\Common7\IDE

适用于 Professional 版或

\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE

适用于 Enterprise 版。

在以前的 Visual Studio 版本中，该文件位于以下位置：

\Program Files (x86)\Common Files\Microsoft Shared\TextTemplating\{version}

其中，{version} 取决于之前安装的版本。

::: moniker-end

## <a name="syntax"></a>语法

```
TextTransform [<options>] <templateName>
```

### <a name="parameters"></a>参数

|**Argument**|**说明**|
|-|-|
|`templateName`|标识要转换的模板文件的名称。|

|**选项**|**说明**|
|-|-|
|-out \<filename>|转换的输出将写入的文件。|
|-r \<assembly>|用于编译和运行文本模板的程序集。|
|-u \<namespace>|用于编译模板的命名空间。|
|-I \<includedirectory>|包含指定文本模板中包含的文本模板的目录。|
|-P \<referencepath>|搜索文本模板中指定的程序集的目录或使用 -r 选项的目录。<br /><br /> 例如，若要包括用于 Visual Studio API 的程序集，请使用<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|-dp \<processorName>!\<className>!\<assemblyName&#124;codeBase>|文本模板中可用来处理自定义指令的指令处理器的名称、完整类型名称和程序集。|
|-a [processorName]![directiveName]!\<parameterName>!\<parameterValue>|指定指令处理器的参数值。 如果只指定参数名称和值，那么参数将可用于所有指令处理器。 如果指定指令处理器，那么参数仅可用于指定的处理器。 如果指定指令名称，那么参数只能在处理特定指令时可用。<br /><br /> 若要从指令处理器或文本模板访问参数，请使用 [ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\))。 在文本模板中，将 `hostspecific` 包含在模板指令中，并在 `this.Host` 上调用消息。 例如：<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`.<br /><br /> 始终键入“!”标记，即使省略可选处理器和指令名称也是如此。 例如：<br /><br /> `-a !!param!value`|
|**-h**|提供帮助。|

## <a name="related-topics"></a>相关主题

|任务|主题|
|-|-|
|在 Visual Studio 解决方案中生成文件。|[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|编写指令处理器转换自己的数据源。|[自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)|
|通过编写文本模板主机，可以从你自己的应用程序调用文本模板。|[使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)|
