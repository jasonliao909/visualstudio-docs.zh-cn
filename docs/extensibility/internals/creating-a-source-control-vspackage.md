---
title: 创建源代码管理 VSPackage |Microsoft Docs
description: 了解如何创建源代码管理 VSPackage，以创建深度集成路径，使源代码管理与Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], creating source control packages
- source control packages
ms.assetid: cca0a9ed-48ff-409f-8036-ed8db0f7533e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e45d798dab342bb50084b467f56f719523ec1df4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086711"
---
# <a name="create-a-source-control-vspackage"></a>创建源代码管理 VSPackage
本文档包含指向与 集成的源代码管理包的体系结构概述的链接、要实现的接口定义的 API 以及要使用的服务，以及演示简单源代码管理包实现的示例。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]

 使用源代码管理 VSPackage，可以创建一个深度集成路径，使源代码管理与 集成 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 它使包能够绕过 承载的默认源代码管理 UI，响应来自项目系统的源代码管理请求 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **，并与组件（如** 解决方案资源管理器）。 [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)]为合作伙伴 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供创建 VSPackage 的机制，该 VSPackage 可以与使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 服务模型集成。

## <a name="in-this-section"></a>本节内容
- [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)

 讨论源代码管理包，它是源代码管理插件的更高级替代方法，用于实现 中的源代码管理功能 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [体系结构](../../extensibility/internals/source-control-vspackage-architecture.md)

 显示关系图并说明源代码管理包的组件。

- [功能](../../extensibility/internals/source-control-vspackage-features.md)

 介绍源代码管理包的各种功能。

- [设计元素](../../extensibility/internals/source-control-vspackage-design-elements.md)

 描述源代码管理包必须实现进行深度集成的 VSPackage 结构。

## <a name="related-sections"></a>相关章节
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)

 讨论如何创建源代码管理插件，该插件在源代码管理用户界面中提供源代码管理 (UI [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]) 。

- [源代码管理](../../extensibility/internals/source-control.md)

 讨论将源代码管理作为 的集成功能实现的选项 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。
