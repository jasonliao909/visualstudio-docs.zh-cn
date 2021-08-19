---
title: Project键入 Essentials |Microsoft Docs
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
ms.openlocfilehash: 251b9f9b17e5e20e7a2d039a77155bd2be457388
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117834"
---
# <a name="project-type-essentials"></a>项目类型基础知识
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 包括多种语言项目类型，例如 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 或 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 还允许创建自己的项目类型。

 如果只想将自定义命令、编辑器或工具窗口添加到 ，则无需 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 创建新项目类型即可这样做。 有关详细信息，请参阅以下主题：

- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

- [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)

- [扩展和自定义工具窗口](../../extensibility/extending-and-customizing-tool-windows.md)

  同样，如果要自定义提供的 和 项目类型的行为，可以使用项目 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 子类型来这样做。 有关详细信息，请参阅子[Project类型](../../extensibility/internals/project-subtypes.md)。

  如果想支持以下一种或多个语言，则必须为基于 和 语言的项目 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 创建新 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目类型：

- 构建

- 部署

- 多个配置

- 源代码管理

- 调试

- Project项解决方案资源管理器

- "**打开Project"** 或 **"Project"** 对话框

- Project嵌套

- 有关项目类型功能的信息，请参阅以下内容：

- Project类型是 VSPackage 中实现一组接口预期 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的对象。 如果使用 C# 开发项目类型，托管包框架项目类将实现所需的接口，并让你继承该实现。 有关详细信息，请参阅[使用托管包框架实现 Project 类型 (C#) 。 ](../../extensibility/internals/using-the-managed-package-framework-to-implement-a-project-type-csharp.md)

- 对于 C++ 开发人员，HierUtil 库中的类以类似方式工作。 有关详细信息，请参阅不在生成中：使用[HierUtil7 ](/previous-versions/bb166212(v=vs.100))Project 类实现 Project 类型 (C++) 。

- Project类型可以支持生成到程序集或程序集中的典型源代码.exe.dll数据。 例如，数据库项目包含对磁盘上存储的脚本和查询文件的引用，并且向 解决方案资源管理器 添加命令以对数据库执行脚本和查询，但项目不支持生成 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 行为。  有关详细信息，请参阅[打开和保存Project项。](../../extensibility/internals/opening-and-saving-project-items.md)

- 项目类型完全不需要使用文件。 例如，项目类型可以在数据库中存储其所有数据。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 使项目类型可以完全控制它们如何持久保存项目和项目项的数据。 有关详细信息，请参阅类型[Project决策](../../extensibility/internals/project-type-design-decisions.md)。

- Project必须提供项目工厂 *，即* 每当系统要求打开或创建基于该项目类型的项目时，创建项目类型的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 实例的对象。 有关详细信息，请参阅使用[Project 工厂创建Project实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。

- Project类型必须为项目和项目项提供模板。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 在用户创建新项目以及将新项添加到现有项目时使用这些模板。 有关详细信息，请参阅[添加Project和Project项模板。](../../extensibility/internals/adding-project-and-project-item-templates.md)

- Project类型可以支持多个配置，例如"调试"和"发布"。 用户可以使用提供的属性页更改项目的不同配置。 有关详细信息，请参阅管理 [配置选项](../../extensibility/internals/managing-configuration-options.md)。

## <a name="see-also"></a>请参阅
- [部署项目类型](../../extensibility/internals/deploying-project-types.md)