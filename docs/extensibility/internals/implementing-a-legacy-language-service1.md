---
title: 实现旧版语言服务 1 |Microsoft Docs
description: 了解如何通过使用 MPF 中的托管包框架实现支持扩展语言服务功能 (语言) 。 第 1 部分（第 2 部分）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services, managed
ms.assetid: df638f24-166d-4b80-be82-c9c39ca7a556
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e7800599529157c9bcd7466f5cad21b3a826c83e371adfed9496b8b6135eca32
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337911"
---
# <a name="implementing-a-legacy-language-service-1"></a>实现旧版语言服务 1
可以使用 MPF (包框架中的类) 实现支持各种功能（如语法突出显示、大括号匹配和 IntelliSense 完成）的旧语言服务。

 旧版语言服务作为 VSPackage 的一部分实现，但实现语言服务功能的较新方式是使用 MEF 扩展。 若要详细了解实现语言服务的新方法，请参阅编辑器 [和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 建议尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并让你能够利用新的编辑器功能。

## <a name="in-this-section"></a>本节内容
- [旧版语言服务概述](../../extensibility/internals/legacy-language-service-overview.md)

 MPF 中支持的语言服务功能的概述。

- [实现旧版语言服务](../../extensibility/internals/implementing-a-legacy-language-service2.md)

 介绍使用 MPF 实现语言服务所需的操作。

- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)

 介绍向 注册基于 MPF 的语言服务所需的步骤 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [旧版语言服务分析器和扫描程序](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)

 介绍使用 MPF 实现语言服务的所有功能所需的两个分析器。

- [演练：创建旧版语言服务](../../extensibility/internals/walkthrough-creating-a-legacy-language-service.md)

 提供在 VSPackage 中实现 MPF 语言服务所需的基本步骤。

- [演练：获取包含已安装的代码片段的列表（旧版实现）](../../extensibility/internals/walkthrough-getting-a-list-of-installed-code-snippets-legacy-implementation.md)

 演示检索已安装代码片段列表的技术。

- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)

 提供指向主题的链接，这些主题详细说明了使用 MPF 实现语言服务的所有功能必须执行哪些操作。
