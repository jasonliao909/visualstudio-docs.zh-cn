---
title: 编辑器和语言服务扩展|Microsoft Docs
description: 可以扩展代码编辑器Visual Studio功能，该编辑器是使用 Windows Presentation Foundation实现的，以托管代码编写。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK]
ms.assetid: 5653bac9-724f-4948-a820-68ce6aa96365
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: cec77762a356f86d8cab32402c824ec70ae41e8e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602360"
---
# <a name="editor-and-language-service-extensions"></a>编辑器和语言服务扩展
可以扩展代码编辑器Visual Studio功能。 编辑器基于 WPF Windows Presentation Foundation (，) 托管代码编写。 尽管此设计不同于早期版本的 Visual Studio，但它提供了大多数相同的功能。 若要扩展编辑器，请使用 Managed Extensibility Framework (MEF) 。

 该Visual Studio SDK 提供称为 *填充* 码的适配器，以支持为早期版本编写的 VSPackage。 不过，如果你有现有的 VSPackage，我们建议将其更新为新技术，以获得更好的性能和可靠性。

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)|使用编辑器项模板的简介。|
|[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)|指向介绍核心编辑器的设计和功能并展示如何扩展它的文档的链接。|
|[编辑器中的旧接口](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015)|指向说明如何从现有代码访问核心编辑器的文档的链接。|
|[创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)|指向说明如何创建自定义编辑器的文档的链接。|
|[旧版语言服务扩展性](../extensibility/internals/legacy-language-service-extensibility.md)|文档链接，这些文档描述如何将编程语言集成到 Visual Studio。|
|[Managed Extensibility Framework (MEF)](/dotnet/framework/mef/index)|介绍 MEF Managed Extensibility Framework () 。|
|[Windows Presentation Foundation](/dotnet/framework/wpf/index)|介绍 WPF Windows Presentation Foundation () 。|
