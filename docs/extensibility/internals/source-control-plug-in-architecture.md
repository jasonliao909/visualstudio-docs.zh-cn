---
title: 源代码管理插件体系结构|Microsoft Docs
description: 了解如何通过实现和附加源代码管理插件Visual Studio IDE 添加源代码管理支持。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3e77815e04604e4818afb8d3f81d1cfd14830fd89ab095dd24df92fb6e57331f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275211"
---
# <a name="source-control-plug-in-architecture"></a>源代码管理插件体系结构
可以通过实现和附加源代码管理插件 (IDE) 集成开发环境 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 添加源代码管理支持。 IDE 通过定义明确的源代码管理 api 连接到源代码Plug-In插件。 IDE 通过提供用户界面来公开源代码管理系统的版本控制功能， (用户界面) 工具栏和菜单命令组成。 源代码管理插件实现源代码管理功能。

## <a name="source-control-plug-in-resources"></a>源代码管理插件资源
 源代码管理插件提供有助于创建版本控制应用程序以及将其连接到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 的资源。 源代码管理插件包含必须由源代码管理插件实现的 API 规范，以便它可以集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 中。 它还包含以 C++ (编写的代码示例) 该代码示例实现了一个主干源代码管理插件，演示了符合源代码管理插件 API 的基本函数的实现。

 如果创建源代码管理 DLL 时具有根据源代码管理插件 API 实现所需的一组函数，源代码管理插件 API 规范允许利用你选择的任何源代码管理系统。

## <a name="components"></a>组件
 关系图中的源代码管理适配器包是 IDE 的组件，该组件将用户对源代码管理操作的请求转换为源代码管理插件支持的函数调用。 为此，IDE 和源代码管理插件必须具有一个有效的对话框，该对话框在 IDE 和插件之间来回传递信息。 若要进行此对话，两者必须使用相同的语言。 本文档中概述的源代码管理插件 API 是此交换的常见词汇。

 ![源代码管理体系结构关系图](../../extensibility/internals/media/vs_sccsdk_plug_in_arch.gif "vs_sccsdk_plug_in_arch") 显示 VS 和源代码管理插件之间的交互的体系结构关系图

 如体系结构图所示，在关系图中标记为 VS shell 的 shell 托管用户的工作项目和关联的组件， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 例如编辑器和解决方案资源管理器。 源代码管理适配器包处理 IDE 和源代码管理插件之间的交互。 源代码管理适配器包提供其自己的源代码管理 UI。 它是用户为了启动和定义源代码管理操作的范围而与之交互的顶级 UI。

 源代码管理插件可以有其自己的 UI，该 UI 可能包含两个部分，如图所示。 标记为"供应商 UI"的框表示作为源代码管理插件创建者提供的自定义用户界面元素。 当用户调用高级源代码管理操作时，源代码管理插件会直接显示这些控件。 标记为"帮助程序 UI"的框是一组源代码管理插件 UI 功能，通过 IDE 间接调用。 源代码管理插件通过 IDE 提供的特殊回调函数将 UI 相关消息传递给 IDE。 帮助程序 UI 通常使用"高级"按钮 (帮助程序 UI 实现与 IDE) 更无缝的集成，从而提供更加统一的最终用户体验。

 源代码管理插件不能对 shell 进行更改，因此不能更改源代码管理适配器包或 IDE 提供的源代码管理 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] UI。 它必须充分利用通过实现各种源代码管理插件 API 函数提供的灵活性，这些函数有助于为最终用户提供集成体验。 源代码管理插件 API 文档的参考部分包含一些高级源代码管理插件功能的信息。 若要利用这些功能，源代码管理插件必须在初始化期间向 IDE 声明其高级功能，并且必须针对每个功能实现特定的高级功能。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../../extensibility/source-control-plug-ins.md)
- [术语表](../../extensibility/source-control-plug-in-glossary.md)
- [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
