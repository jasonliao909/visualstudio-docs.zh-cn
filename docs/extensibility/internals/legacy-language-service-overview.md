---
title: 旧版语言服务概述|Microsoft Docs
description: 了解中旧版语言服务Visual Studio以及托管包框架支持的功能 (MPF) 语言服务类。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], about language services
ms.assetid: bb44e27b-d228-463c-b2cf-cd5c24c7c1b5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d129e02dec3770a1a2288c68ff99d6b6ac2cf0a4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042265"
---
# <a name="legacy-language-service-overview"></a>旧版语言服务概述
语言服务提供编辑器支持，使你能够实现某些 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 功能。 托管包框架 (MPF) 语言服务类提供对常用功能的完全支持，并部分支持其他功能。

## <a name="fully-supported-features-in-the-mpf"></a>MPF 中完全支持的功能
 MPF 语言服务类支持以下功能：

- 语法突出显示

- 大纲显示

- 对代码块进行注释

- 大括号匹配

- 代码片段

- 自定义文档属性

- IntelliSense 参数信息

- IntelliSense 快速信息

- IntelliSense 成员完成

- IntelliSense 单词完成

## <a name="partially-supported-features-in-the-mpf"></a>MPF 中部分支持的功能
 MPF 仅对以下功能提供部分支持。 这意味着必须实现 MPF 调用的方法。

- 重新格式化代码。 提供实现重新格式化的代码。

- 通过标识有效的代码范围来验证断点。 提供用于标识代码范围的代码。

- 支持调试器 **"自动"** 窗口以显示变量。 提供确定要显示在窗口中的代码。

- 支持导航 **栏，** 以在类型和成员之间快速导航。 实现并返回一个帮助程序类，该类填充导航栏组合 **框中** 的列表。

## <a name="implementation"></a>实现
 必须完成几个步骤，实现语言服务本身以及想要支持语言的语言服务功能。 下列主题将讨论这些步骤：

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

- [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)

- [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

- [旧版语言服务中的大纲显示](../../extensibility/internals/outlining-in-a-legacy-language-service.md)

- [在旧版语言服务中注释代码](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)

- [在旧版语言服务中重新格式化代码](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)

- [在旧版语言服务中自定义文档属性](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)

- [旧版语言服务中的代码片段支持](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)

- [旧版语言服务中的导航栏支持](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)

- [旧版语言服务中的文字完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)

- [旧版语言服务中的成员完成](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)

- [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)

- [旧版语言服务中的快速信息](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)

- [旧版语言服务中的自动窗口支持](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)

- [验证旧版语言服务中的断点](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)

## <a name="see-also"></a>请参阅
- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)
