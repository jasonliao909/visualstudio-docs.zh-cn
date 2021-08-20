---
title: 使用 TextTransform 实用工具生成文件
description: 了解 TextTransform 实用工具如何是可用于转换文本模板的命令行工具。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122085606"
---
# <a name="generate-files-with-the-texttransform-utility"></a>使用 TextTransform 实用工具生成文件

TextTransform.exe是一个命令行工具，可用于转换文本模板。 调用 TextTransform.exe时，将文本模板文件的名称指定为参数。 TextTransform.exe调用文本转换引擎并处理文本模板。 TextTransform.exe通常从脚本调用 。 但是，它通常不是必需的，因为可以在生成过程中执行Visual Studio转换。

> [!NOTE]
> 如果要在生成过程中执行文本转换，请考虑使用MSBuild转换任务。 有关详细信息，请参阅生成 [过程中的代码生成](../modeling/code-generation-in-a-build-process.md)。 在安装了 Visual Studio 的计算机中，还可以编写可以转换文本Visual Studio的应用程序或扩展。 有关详细信息，请参阅使用 [自定义主机 处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)。

TextTransform.exe位于以下目录中：

::: moniker range=">=vs-2019"

**\Program Files (x86) \Microsoft Visual Studio\2019\Professional\Common7\IDE**

对于 Professional 版本，或

**\Program Files (x86) \Microsoft Visual Studio\2019\Enterprise\Common7\IDE**

对于 Enterprise 版本。

::: moniker-end

::: moniker range="vs-2017"

**\Program Files (x86) \Microsoft Visual Studio\2017\Professional\Common7\IDE**

对于 Professional 版本，或

**\Program Files (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE**

对于 Enterprise 版本。

在早期版本的 Visual Studio 中，该文件位于以下位置：

**\Program Files (x86) \Common Files\Microsoft Shared\TextTemplating \{ version}**

其中 {version} 取决于安装的以前版本。

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
|**-out**\<filename>|将转换的输出写入的文件。|
|**-r**\<assembly>|用于编译和运行文本模板的程序集。|
|**-u**\<namespace>|用于编译模板的命名空间。|
|**-I**\<includedirectory>|包含指定文本模板中包含的文本模板的目录。|
|**-P**\<referencepath>|用于搜索文本模板中指定的程序集或用于使用 **-r** 选项的目录。<br /><br /> 例如，若要包含用于 Visual Studio API 的程序集，请使用<br /><br /> `-P "%VSSHELLFOLDER%\Common7\IDE\PublicAssemblies"`|
|**-dp** \<processorName> \<className> ！ ！\<assemblyName&#124;codeBase>|可用于处理文本模板中的自定义指令的指令处理器的名称、完整类型名称和程序集。|
|**-a** [processorName]！[directiveName]！ \<parameterName> ！\<parameterValue>|指定指令处理器的参数值。 如果仅指定参数名称和值，则参数将可供所有指令处理器使用。 如果指定指令处理器，则参数仅适用于指定的处理器。 如果指定指令名称，则参数仅在处理指定的指令时可用。<br /><br /> 若要从指令处理器或文本模板访问参数值，请使用 [ITextTemplatingEngineHost.ResolveParameterValue](/previous-versions/visualstudio/visual-studio-2012/bb126369\(v\=vs.110\))。 在文本模板中， `hostspecific` 在模板指令中包括 并调用 上的消息 `this.Host` 。 例如：<br /><br /> `<#@template language="c#" hostspecific="true"#> [<#= this.Host.ResolveParameterValue("", "", "parameterName") #>]`.<br /><br /> 即使省略可选的处理器和指令名称，也始终键入"！"标记。 例如：<br /><br /> `-a !!param!value`|
|-h|提供帮助。|

## <a name="related-topics"></a>相关主题

|任务|主题|
|-|-|
|在解决方案中Visual Studio文件。|[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)|
|编写指令处理器转换自己的数据源。|[自定义 T4 文本转换](../modeling/customizing-t4-text-transformation.md)|
|编写文本模板化主机，用于从自己的应用程序调用文本模板。|[使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)|
