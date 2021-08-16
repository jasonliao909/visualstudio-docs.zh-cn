---
title: T4 输出指令
description: 了解 Visual Studio 文本模板中，output 指令用于定义转换文件的文件扩展名和编码。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 24578c6bbc9bf5953dcfc4b05bc3118c22447a47e9353c1f2268b00985836790
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121271025"
---
# <a name="t4-output-directive"></a>T4 输出指令

在 Visual Studio 文本模板中， `output` 指令用于定义转换文件的文件扩展名和编码。

 例如，如果 Visual Studio 项目包含名为 **MyTemplate.tt** 的模板文件，其中包含以下指令：

 `<#@output extension=".cs"#>`

 然后 Visual Studio 会生成一个名为 **MyTemplate** 的文件

 运行时（预处理）文本模板中不需要 `output` 指令。 相反，应用程序通过调用 `TextTransform()` 来获取已生成的字符串。 有关详细信息，请参阅[使用 T4 文本模板的运行时文本生成](../modeling/run-time-text-generation-with-t4-text-templates.md)。

## <a name="using-the-output-directive"></a>使用输出指令

```
<#@ output extension=".fileNameExtension" [encoding="encoding"] #>
```

 每个文本模板中不应该有多个 `output`。

## <a name="extension-attribute"></a>extension 特性
 指定生成的文本输出文件的文件扩展名。

 默认值为 **.cs**

 示例：`<#@ output extension=".txt" #>`

 `<#@ output extension=".htm" #>`

 `<#@ output extension=".cs" #>`

 `<#@ output extension=".vb" #>`

 可接受的值：任何有效的文件扩展名。

## <a name="encoding-attribute"></a>编码属性
 指定生成输出文件时要使用的编码。 例如：

 `<#@ output encoding="utf-8"#>`

 默认值为文本模板文件使用的编码。

 可接受的值： `us-ascii`

 `utf-16BE`

 `utf-16`

 `utf-8`

 `utf-7`

 `utf-32`

 `0` (系统默认) 

 一般情况下，可以使用 WebName 字符串或 <xref:System.Text.Encoding.GetEncodings%2A?displayProperty=fullName> 返回的任一编码的 CodePage 编号。
