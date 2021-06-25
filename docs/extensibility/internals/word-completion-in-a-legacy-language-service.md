---
title: 旧版语言服务中的单词完成|Microsoft Docs
description: 可以在 Visual Studio SDK 中为旧版语言服务Visual Studio完成。 了解如何在 VSPackage 中实现旧版语言服务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services [managed package framework], IntelliSense Complete Word
- IntelliSense, Complete Word
- Complete Word
ms.assetid: 0ace5ac3-f9e1-4e6d-add4-42967b1f96a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ea386aea3a17b0fb0d93ff9872f92e86a166be5c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902626"
---
# <a name="word-completion-in-a-legacy-language-service"></a>旧版语言服务中的文字完成
单词完成在部分键入的单词上填充缺少的字符。 如果只有一个可能的完成，则输入完成字符时完成单词。 如果部分单词与多个可能匹配，则显示可能的完成列表。 完成字符可以是不用于标识符的任何字符。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要了解更多信息，请参阅 [扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

## <a name="implementation-steps"></a>实现步骤

1. 当用户从 **IntelliSense** 菜单中选择"完成 **Word"** 时， <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 该命令将发送到语言服务。

2. <xref:Microsoft.VisualStudio.Package.ViewFilter>类捕获 命令，并调用具有 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> 分析原因的 方法 <xref:Microsoft.VisualStudio.Package.ParseReason> 。

3. 然后， 类调用 方法获取可能的单词完成列表，然后使用 类在工具 <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 提示列表中显示 <xref:Microsoft.VisualStudio.Package.CompletionSet> 单词。

    如果只有一个匹配的单词， <xref:Microsoft.VisualStudio.Package.Source> 类将完成该单词。

   或者，如果扫描程序在键入标识符的第一个字符时返回触发器值，则 类将检测此值，并调用 方法，其 <xref:Microsoft.VisualStudio.Package.TokenTriggers> <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> 分析原因为 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 在这种情况下，分析器必须检测成员选择字符是否存在并提供成员列表。

## <a name="enabling-support-for-the-complete-word"></a>启用对完整单词的支持
 若要启用对单词完成的支持，设置传递给与语言包关联的 `CodeSense` <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 用户属性的命名参数。 这会在 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> 类上设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 属性。

 分析器必须返回声明列表以响应分析原因值 <xref:Microsoft.VisualStudio.Package.ParseReason> ，单词完成操作。

## <a name="implementing-complete-word-in-the-parsesource-method"></a>在 ParseSource 方法中实现完整单词
 对于单词完成 <xref:Microsoft.VisualStudio.Package.Source> ，类对 <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> 类调用 方法 <xref:Microsoft.VisualStudio.Package.AuthoringScope> 以获取可能的单词匹配项的列表。 必须在派生自 类的类中实现 <xref:Microsoft.VisualStudio.Package.Declarations> 列表。 有关 <xref:Microsoft.VisualStudio.Package.Declarations> 必须实现的方法的详细信息，请参阅 类。

 如果列表仅包含一个单词，则 类会自动插入 <xref:Microsoft.VisualStudio.Package.Source> 该单词来表示部分单词。 如果列表包含多个单词，类将显示一个工具提示列表，用户可以 <xref:Microsoft.VisualStudio.Package.Source> 从中选择适当的选项。

 另请看旧版语言服务 <xref:Microsoft.VisualStudio.Package.Declarations> 中的成员完成 [中的类实现示例](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)。
