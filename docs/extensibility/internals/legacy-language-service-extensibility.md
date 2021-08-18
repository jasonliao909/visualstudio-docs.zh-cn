---
title: 旧版语言服务扩展性|Microsoft Docs
description: 了解中旧语言服务的结构、实现和扩展Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services
- Visual Studio, language services
ms.assetid: 2700cd4d-5f68-43fc-b62f-dc80c3f3aa85
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2991ae503add55cfb8f3981eeeba5f2e6c1e0fe8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049839"
---
# <a name="legacy-language-service-extensibility"></a>旧版语言服务扩展性
语言服务为在 IDE 中编辑源代码提供特定于语言的支持。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要详细了解实现语言服务的新方法，请参阅编辑器 [和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

 本部分讨论旧版语言服务的结构和实现。

## <a name="in-this-section"></a>本节内容
- [迁移旧版语言服务](../../extensibility/internals/migrating-a-legacy-language-service.md)

 说明如何将语言服务从 Visual Studio 2008 更新到最新版本。

- [旧版语言服务基础知识](../../extensibility/internals/legacy-language-service-essentials.md)

 提供有关如何开发语言服务以将编程语言集成到 Visual Studio。

- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)

 提供可帮助你创建语言服务的主题的链接。

- [在旧版语言服务中进行语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)

 提供有关支持语言服务中的语法突出显示的信息。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service1.md)

 提供有关如何使用 MPF (包框架) 在托管代码中实现功能齐全的语言服务的信息。

- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 介绍可用于浏览 IDE 中符号的树视图的库和工具。

## <a name="related-sections"></a>相关章节
- [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)

 提供编辑器Visual Studio概述。

- [用于调试的语言服务支持](../../extensibility/internals/language-service-support-for-debugging.md)

 提供有关 调试 SDK 的信息Visual Studio链接，其中包含创建和自定义用于调试程序调试器组件的信息。
