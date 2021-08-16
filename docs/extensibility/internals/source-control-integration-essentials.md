---
title: 源代码管理集成|Microsoft Docs
description: 了解用户支持的两Visual Studio源代码管理集成：源代码管理插件和基于 VSPackage 的源代码管理解决方案。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Source Control Integration, essentials
- Source Control Integration,overview
- essentials, Source Control Integration
ms.assetid: 442057cb-fd54-4283-96f8-2f6dc8bf2de7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 00015c08a95e0fea62911942f996817d115ceaeedc04a677dfc2cc36597d78db
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401162"
---
# <a name="source-control-integration-essentials"></a>源代码管理集成基础知识
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持两种类型的源代码管理集成：提供基本功能的源代码管理插件（使用源代码管理插件 API (以前称为 MSSCCI API) ）和基于 VSPackage 的源代码管理集成解决方案，可提供更可靠的功能。

## <a name="source-control-plug-in"></a>源代码管理插件
 源代码管理插件编写为实现源代码管理插件 API 的 DLL。 注册和源代码管理集成功能通过 API 提供。 此方法比源代码管理 VSPackage 更易于实现，并且它使用用户界面 ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI) 大多数源代码管理操作。

 若要使用源代码管理插件 API 实现源代码管理插件，请执行以下步骤：

1. 创建一个 DLL，用于实现 [源代码管理插件 中指定的函数](../../extensibility/source-control-plug-ins.md)。

2. 按照如何：安装源代码管理插件中所述，通过创建适当的注册表项[来注册 DLL。](../../extensibility/internals/how-to-install-a-source-control-plug-in.md)

3. 创建帮助程序 UI，在源代码管理适配器包提示时显示它 (该组件通过源代码管理插件 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]) 。

   有关详细信息，请参阅 [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)。

## <a name="source-control-vspackage"></a>源代码管理 VSPackage
 使用源代码管理 VSPackage 实现可以开发源代码管理 UI 的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 自定义替换。 此方法提供对源代码管理集成的完整控制，但它要求你提供 UI 元素并实现源代码管理接口，否则将在插件方法下提供这些接口。

 若要实现源代码管理 VSPackage，必须：

1. 如注册和选择中所述，创建并注册自己的源代码 [管理](../../extensibility/internals/registration-and-selection-source-control-vspackage.md)VSPackage。

2. 将默认源代码管理 UI 替换为自定义 UI。 请参阅[自定义用户界面。](../../extensibility/internals/custom-user-interface-source-control-vspackage.md)

3. 指定使用字形， **并处理解决方案资源管理器** 事件。 请参阅 [字形控件](../../extensibility/internals/glyph-control-source-control-vspackage.md)。

4. 处理查询编辑和查询保存事件，如查询编辑 [查询保存中所示](../../extensibility/internals/query-edit-query-save-source-control-vspackage.md)。

   有关详细信息，请参阅 [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)。

## <a name="see-also"></a>另请参阅
- [概述](../../extensibility/internals/source-control-integration-overview.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)
