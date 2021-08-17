---
title: 源代码管理 VSPackage 体系结构|Microsoft Docs
description: 了解源代码管理包的体系结构，该包是一个 VSPackage，它Visual Studio源代码管理服务的功能。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control packages, architecture
ms.assetid: 453125fc-23dc-49b1-8476-94581f05e6c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 02507ef3044e89948b9f852c25f662cb3ad330cd0c94d5fbe3985ff295e28d36
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432134"
---
# <a name="source-control-vspackage-architecture"></a>源代码管理 VSPackage 体系结构
源代码管理包是使用 IDE 提供的服务的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage。 作为返回，源代码管理包提供其作为源代码管理服务的功能。 此外，源代码管理包比源代码管理插件更通用，用于将源代码管理集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中。

 实现源代码管理插件 API 的源代码管理插件遵守严格的协定。 例如，插件不能替换 UI 应用程序 ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 用户界面) 。 此外，源代码管理插件 API 不会启用插件来实现自己的源代码管理模型。 但是，源代码管理包克服了这两个限制。 源代码管理包可以完全控制用户的源代码管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 体验。 此外，源代码管理包可以使用自己的源代码管理模型和逻辑，并可以定义所有与源代码管理相关的用户界面。

## <a name="source-control-package-components"></a>Source-Control包组件
 如体系结构图所示，名为"源代码管理存根"的组件是一个 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage，用于将源代码管理包与 集成 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 源代码管理存根处理以下任务。

- 提供源代码管理包注册所需的通用 UI。

- 加载源代码管理包。

- 将源代码管理包设置为活动/非活动。

  源代码管理存根查找源代码管理包的活动服务，并路由从 IDE 到该包的所有传入服务调用。

  源代码管理适配器包是提供的特殊源代码管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 包。 此包是支持基于源代码管理插件 API 的源代码管理插件的中心组件。 当源代码管理插件是活动插件时，源代码管理存根会将其事件发送到源代码管理适配器包。 反过来，源代码管理适配器包使用源代码管理插件 API 与源代码管理插件通信，并提供所有源代码管理插件通用的默认 UI。

  当源代码管理包是活动包时，另一方面，源代码管理存根使用包接口直接与Source-Control [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] 通信。 源代码管理包负责托管其自己的源代码管理 UI。

  ![源代码管理体系结构图](../../extensibility/internals/media/vsipsccarch.gif "VSIPSCCArch")

  对于源代码管理包， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 不提供源代码管理代码或用于集成的 API。 将其与创建源代码管理插件（其中[](../../extensibility/internals/creating-a-source-control-plug-in.md)源代码管理插件必须实现一组严格的函数和回调）中概述的方法形成对比。

  与任何 VSPackage 一样，源代码管理包是可以使用 创建的 COM 对象 `CoCreateInstance` 。 VSPackage 通过实现 使自身 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 可用于 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage> IDE。 创建实例后，VSPackage 将接收站点指针和接口，该接口提供对 IDE 中可用服务和接口的 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> VSPackage 访问权限。

  与编写基于源代码管理插件 API 的插件相比，编写基于 VSPackage 的源代码管理包需要更高级的编程专业知识。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>
- [入门](../../extensibility/internals/getting-started-with-source-control-vspackages.md)
