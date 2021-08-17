---
title: 源代码管理插件|Microsoft Docs
description: 本节中的文章介绍使源代码管理系统能够与源代码管理集成的完整接口Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, reference
ms.assetid: 964980ca-21c5-4706-8535-6ea23e1c9cc9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: abc8c8f439fa104ae84de8ffdc6f8d96a0909998
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122028639"
---
# <a name="source-control-plug-ins"></a>源代码管理插件
源代码管理插件 SDK 参考部分包含使源代码管理系统能够与 集成的完整接口规范 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 它指定源代码管理插件必须实现的各种函数和数据类型的语法和语义，以与 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE (集成) 。

## <a name="in-this-section"></a>本节内容
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md) 列出必须由源代码管理插件实现以符合源代码管理插件 API 的函数。

- [由 IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md) 描述源代码管理插件在执行某些命令时用于将信息传递回 IDE 的函数。

- [枚举器](../extensibility/enumerators.md) 列出源代码管理插件插件必须了解的源代码管理插件 API 中的枚举器数据类型。

- [功能标志](../extensibility/capability-flags.md) 描述 `SCC_CAP_xxx` 标志，这些标志指示提供程序的功能。

- [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md) 列出特定命令上下文中有用的标志。

- [错误代码](../extensibility/error-codes.md) 将函数返回的常见错误值作为 列出 `SCCTRN` 。

- [用作查找源代码管理插件的密钥的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md) 描述用于访问注册表以查找源代码管理插件的密钥。

- [MSSCCPRJ。SCC 文件](../extensibility/mssccprj-scc-file.md) 描述一个客户端文件，该文件包含对 IDE 不透明的信息，但源代码管理插件使用该文件在版本控制中查找解决方案或项目。

- [实现源代码管理插件的最佳实践](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md) 提供实现源代码管理插件 API 时需要记住的重要技术提醒的集合。

- [对字符串长度的限制](../extensibility/restrictions-on-string-lengths.md) 介绍源代码管理插件 API 中对各种函数中使用的字符串长度的限制。

- [术语表](../extensibility/source-control-plug-in-glossary.md) 提供有用的术语及其定义，用于阅读源代码管理插件 SDK 文档。

- [如何：关闭源代码管理插件的兼容性警告](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md) 介绍如何禁用警告。

## <a name="related-sections"></a>相关章节
- [源代码管理插件示例](https://www.microsoft.com/download/details.aspx?id=55984) 提供源代码管理插件功能的示例。

- [源代码管理插件测试指南](../extensibility/internals/test-guide-for-source-control-plug-ins.md) 介绍与源代码管理插件相关的测试过程。

- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md) 讨论如何创建源代码管理插件，该插件在使用源代码管理用户界面和 UI (时 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 提供源代码) 。

- [Visual Studio SDK 参考](../extensibility/visual-studio-sdk-reference.md)显示参考主题的列表。
