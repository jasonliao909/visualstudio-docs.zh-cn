---
title: XML 编辑器
description: 了解 Visual Studio 中的 XML 编辑器基于文本编辑器，并增加了对 XML 语言的支持。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-xml-tools
ms.workload:
- multiple
ms.openlocfilehash: aa9411d77b8bdece857a4c63bc96fa04727ceb67
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644564"
---
# <a name="xml-editor"></a>XML 编辑器

Visual Studio 中的“XML 编辑器”基于文本编辑器，并增加了对 XML 语言的支持。 在 Visual Studio 中打开 XML 文件时，它将在 XML 编辑器中打开。

XML 编辑器具有下列功能：

- XML 1.0 语法检查。

- 键入时的架构验证。

- XML 代码段支持，包括从架构生成的代码段。

- 支持文档类型定义 (DTD)。

- 支持 XML 架构定义语言 (XSD) 架构。

- 从 XML 实例文档创建 XML 架构。

- 将 DTD 或 XML 数据简化 (XDR) 架构转换为 XML 架构。

- XSLT 语法检查。

- 文档以大纲方式显示，从而使得可以展开和折叠元素。

- 与 [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)集成。 这可提供 XML 架构的分层视图。

将为 .xml、.xsd、.xsl 和 .config 等常见的文件扩展名调用 XML 编辑器   。如果文件似乎包含 XML，未知的文件扩展名也会调用 XML 编辑器。

## <a name="xslt-intellisense"></a>XSLT IntelliSense

通过 [XSLT IntelliSense](../xml-tools/xml-editor-intellisense-features.md)，可以自动填充特性集名称、模板模式和名称以及指定模式或指定命名模板的参数名。

## <a name="xslt-profiler"></a>XSLT 探查器

[XSLT 探查器](../xml-tools/xslt-profiler.md)可创建详细的 XSLT 性能报告，有助于度量、评估和锁定 XSLT 代码中与性能相关的问题。 XSLT 探查器还包含有关 XSL 和 XSLT 样式表优化的有用提示。

## <a name="xslt-hierarchy"></a>XSLT 层次结构

[XSLT 层次结构工具](../xml-tools/walkthrough-using-xslt-hierarchy.md)允许在包含的样式表和/或内置模板规则中添加断点。

## <a name="see-also"></a>请参阅

- [XML 编辑器选项 - 格式设置](../ide/reference/options-text-editor-xml-formatting.md)
- [XML 编辑器选项 - 杂项](../ide/reference/options-text-editor-xml-miscellaneous.md)
- [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)
- [XML 标准参考](/previous-versions/dotnet/netframework-4.0/ms256177(v=vs.100))
- [Visual Studio 中的 XML 工具](../xml-tools/xml-tools-in-visual-studio.md)