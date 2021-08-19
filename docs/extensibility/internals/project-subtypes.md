---
title: Project子类型|Microsoft Docs
description: 了解项目子类型如何让你自定义项目系统的行为Visual Studio。 VSPackage 使用 COM 聚合实现项目子类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], subtypes
- project subtypes [Visual Studio SDK]
ms.assetid: d235b47b-cf11-4d47-a63f-e33d9d16105d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6b625e35b74293006f7f695629ae09b990d4cb40
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063039"
---
# <a name="project-subtypes"></a>项目子类型
Project子类型，可自定义或修改 的项目系统的行为 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 自定义项包括在项目文件中保存其他数据、在"添加新项"对话框中添加或筛选项、控制如何调试和部署程序集，以及扩展项目"属性 **页"** 对话框。 VSPackage 使用 COM 聚合实现项目子类型。

> [!NOTE]
> Visual C++项目系统不支持项目子类型。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]本身使用项目子类型来实现SQL Server智能设备项目。

## <a name="in-this-section"></a>本节内容

- [项目子类型设计](../../extensibility/internals/project-subtypes-design.md)

  介绍项目子类型的概念。

- [项目子类型的初始化序列](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)

  按环境描述编程项目子类型初始化 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 序列。

- [项目子类型扩展的属性和方法](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)

  提供使用项目子类型最常扩展的功能和方法的详细说明。

- [保留 MSBuild 项目文件中的数据](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)

  描述如何在项目文件中保存数据，以及如何使用 在项目子类型聚合级别中维护 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> 项目文件的数据。

- [项目属性用户界面](../../extensibility/internals/project-property-user-interface.md)

  描述项目子类型如何修改项目 **"属性页"** 对话框。

- [扩展基项目的对象模型](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)

  提供有关项目子类型如何使用自动化扩展程序扩展自动化对象模型的信息。

- [构成“添加新项”对话框](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)

  介绍如何将项添加到" **添加新项"** 对话框。

- [将数据保存在项目文件中](../../extensibility/saving-data-in-project-files.md)

  介绍项目子类型如何使用 MPF 中的托管包框架在项目文件中保存和检索 (子) 。

- [处理专用部署](../../extensibility/internals/handling-specialized-deployment.md)

  说明项目子类型如何通过实现 接口提供专用部署 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> 行为。

- [添加和删除属性页](../../extensibility/adding-and-removing-property-pages.md)

  介绍如何在设计器中添加和删除Project页。

## <a name="related-sections"></a>相关章节

- [项目类型](../../extensibility/internals/project-types.md)

  提供指向详细介绍项目 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的主题的链接。
