---
title: Project类型基础 |Microsoft Docs
description: 了解何时必须创建项目类型，以及何时可以使用项目子类型扩展现有项目类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project types [Visual Studio SDK]
ms.assetid: 09991589-2300-430e-b6a4-7f2b95fe676f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 758cc981e1c202f28693d780dbc06089a061d9984b2f7208d5da983c0922d080
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401368"
---
# <a name="project-type-essentials"></a>项目类型基础知识
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 包含多种语言的项目类型，如 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 或 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 还允许您创建自己的项目类型。

 如果只是想要将自定义命令、编辑器或工具窗口添加到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，则可以执行此操作，而无需创建新的项目类型。 有关详细信息，请参阅以下主题：

- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

- [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)

- [扩展和自定义工具窗口](../../extensibility/extending-and-customizing-tool-windows.md)

  同样，如果要自定义所提供的 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目类型的行为，则可以使用项目子类型执行此操作。 有关详细信息，请参阅[Project 子类型](../../extensibility/internals/project-subtypes.md)。

  [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 如果要支持下列一项或多项操作，则必须为基于和以外的其他语言的项目创建新的项目类型：

- 构建

- 部署

- 多个配置

- 源代码管理

- 调试

- Project 解决方案资源管理器中的项

- "**打开 Project** " 或 "**新建 Project** " 对话框

- Project 嵌套

- 有关项目类型的功能的详细信息，请参阅以下内容：

- Project 类型是实现接口所需的 VSPackage 中的对象 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 如果使用 c # 开发项目类型，托管包框架项目类将实现所需的接口，并使你能够继承该实现。 有关详细信息，请参阅[使用托管包框架实现 (c # ) 的 Project 类型](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md)。

- 对于 c + + 开发人员而言，HierUtil 库中的类的工作方式类似。 有关详细信息，请参阅[不在生成中：使用 HierUtil7 Project 类实现 Project 类型 (c + +) ](/previous-versions/bb166212(v=vs.100))。

- Project 类型可以支持内置于 .exe 或 .dll 程序集中的典型源代码文件以外的数据。 例如， [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 数据库项目包含对存储在磁盘上的脚本和查询文件的引用，并向 **解决方案资源管理器** 添加命令以对数据库执行脚本和查询，但这些项目不支持生成行为。 有关详细信息，请参阅[打开和保存 Project 项](../../extensibility/internals/opening-and-saving-project-items.md)。

- 项目类型根本不必使用文件。 例如，项目类型可以将其所有数据存储在数据库中。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使项目类型完全控制其如何保存项目和项目项的数据。 有关详细信息，请参阅[Project 类型设计决策](../../extensibility/internals/project-type-design-decisions.md)。

- Project 类型必须提供一个 *项目工厂*，这是一个对象，该对象在每次 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 被告知打开或创建基于该项目类型的项目时都创建项目类型的实例。 有关详细信息，请参阅[使用 Project 工厂创建 Project 实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。

- Project 类型必须提供项目和项目项的模板。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 用户创建新项目并向现有项目中添加新项时使用模板。 有关详细信息，请参阅[添加 Project 和 Project 项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

- Project 类型可以支持多个配置，例如调试和发布。 用户可以使用所提供的属性页更改项目的不同配置。 有关详细信息，请参阅 [管理配置选项](../../extensibility/internals/managing-configuration-options.md)。

## <a name="see-also"></a>另请参阅
- [部署项目类型](../../extensibility/internals/deploying-project-types.md)