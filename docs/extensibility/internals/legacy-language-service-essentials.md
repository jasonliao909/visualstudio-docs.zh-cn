---
title: 旧版语言服务 Essentials |Microsoft Docs
description: 了解旧版语言服务中提供的基本功能，这些功能允许你将编程语言集成到Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- languages, integrating into Visual Studio
- language services, integrating programming languages
- Visual Studio, integrating programming languages
- programming languages, integrating into Visual Studio
ms.assetid: c15e0ccb-e7c5-4dbb-affb-fe3d3244debe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: dda53c2ea5c282e67b3ed0ec86112a2a69d64cab
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049904"
---
# <a name="legacy-language-service-essentials"></a>旧版语言服务基础知识
必须提供语言服务，将编程语言集成到 Visual Studio。 本主题介绍旧版语言服务中提供的功能。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要详细了解实现语言服务的新方法，请参阅编辑器 [和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

 旧版语言服务提供以下功能：

|Feature|说明|
|-------------|-----------------|
|语法着色|使编辑器视图为语言的不同元素显示不同的颜色和字体样式。 这种差异可以更轻松地读取和编辑文件。<br /><br /> 有关常规信息，请参阅 [旧版语言服务 中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。<br /><br /> 有关 MPF 的托管包框架 (中) ，请参阅旧版语言服务 中的 [语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。|
|语句结束|完成用户已开始键入的语句或关键字。 语句完成可帮助用户更轻松地输入困难语句，减少键入错误的可能性。<br /><br /> 有关常规信息，请参阅 [旧版语言服务 中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)。<br /><br /> 有关 MPF 中的此功能的信息，请参阅 [旧版语言服务 中的单词完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)。|
|大括号匹配|突出显示大括号等配对字符。 当用户输入结束字符（如"}"）时，大括号匹配会突出显示相应的开始字符，例如"{"。 当存在多个级别的封闭字符时，此功能可帮助用户确认封闭字符已正确配对。<br /><br /> 有关 MPF 中的此功能的信息，请参阅旧版 [语言服务 中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)。|
|参数信息工具提示|显示用户当前正在键入的重载方法的可能签名的列表。<br /><br /> 有关常规信息，请参阅 [旧版语言服务 中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)。<br /><br /> 有关 MPF 中的此功能的信息，请参阅 [旧版语言服务 中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)。|
|错误标记|在语法不正确的文本下显示波浪红色下划线（也称为波浪线）。 错误标记通常用于让用户了解拼写错误的关键字、未圆括号、无效字符和类似错误。<br /><br /> 在 MPF 类中，错误标记在 类的 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> 方法中自动 <xref:Microsoft.VisualStudio.Package.AuthoringSink> 处理。|

 其中许多功能需要语言服务来分析源代码。 通常可以重复使用编译器或解释器标记化和分析代码。

 以下功能与编程语言支持相关，但不是语言服务的一部分：

| Feature | 说明 |
|-----------------------| - |
| 表达式评估器 | 通过验证断点和提供表达式列表以在"自动调试"窗口中显示，支持 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 调试器。 <br /><br /> 有关详细信息，请参阅 [语言服务对调试的支持](../../extensibility/internals/language-service-support-for-debugging.md)。 |
| 符号浏览工具 | 支持 **对象浏览器** **、类视图、调用浏览器** 和 **查找符号结果**。  |
