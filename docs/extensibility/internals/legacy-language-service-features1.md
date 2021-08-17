---
title: 旧版语言服务功能1 |Microsoft Docs
description: 了解 MPF Visual Studio 语言服务的托管包框架 (支持) 功能。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework]
ms.assetid: a646e4f0-767d-4cd1-8e1a-9a2aa210a1b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 94099df26da9d9fcd62db62ad440820056775a81
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042278"
---
# <a name="legacy-language-service-features-1"></a>旧版语言服务功能 1
MPF 语言 (包) 框架可以支持一个或多个功能，例如语法突出显示 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 、IntelliSense 和断点验证。 每个功能都可以独立于其他功能实现，但除语法突出显示（只需要扫描程序）外，所有功能都需要分析器与扫描程序。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

 描述支持语言对匹配（也称为大括号匹配）所需的内容。

- [在旧版语言服务中注释代码](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

 描述支持对所选代码进行注释和取消注释所需的操作。

- [在旧版语言服务中自定义文档属性](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

 描述支持嵌入在源文件中的文档属性所需的内容。

- [旧版语言服务中的大纲显示](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

 描述通过实现隐藏区域来支持大纲显示所需的操作。

- [在旧版语言服务中重新格式化代码](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

 描述支持重新格式化代码所需的项。

- [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

 描述支持代码片段（即插入并可以编辑的代码段）所需的内容。

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

 描述在键入方法时支持用于显示方法签名的 IntelliSense 参数信息操作所需的内容。

- [旧版语言服务中的快速信息](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

 描述支持 IntelliSense 快速信息操作显示有关标识符的信息所需的内容。

- [旧版语言服务中的成员完成](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

 描述支持从列表中选择命名空间的成员的 IntelliSense 成员完成操作所需的内容。

- [旧版语言服务中的文字完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

 描述支持 IntelliSense 完成单词操作以完成部分键入的单词所需的内容。

- [旧版语言服务中的自动窗口支持](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

 介绍语言服务在调试时可以执行 **哪些操作来支持** "自动"窗口。

- [旧版语言服务中的导航栏支持](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

 介绍如何使用编辑器 **视图** 顶部的导航栏快速导航到该视图中显示的文件中的任何类型或成员。

- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

 描述支持源代码的语法突出显示所需的内容。

- [验证旧版语言服务中的断点](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

 描述语言服务可以执行哪些工作来支持在调试器外部验证断点。

## <a name="related-sections"></a>相关章节
- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 描述实现使用托管包框架的语言服务的所有功能所需的分析和扫描程序。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 介绍使用 MPF 实现语言服务所需的操作。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

 介绍向 注册基于 MPF 的语言服务所需的步骤 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [使用 IntelliSense](../../ide/using-intellisense.md)

 说明 IntelliSense 如何使语言引用易于访问。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 提供有关如何使用 MPF (包框架) 在托管代码中实现功能齐全的语言服务的信息。
