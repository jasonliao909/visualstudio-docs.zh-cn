---
title: Project类型|Microsoft Docs
description: Visual Studio包括多种适用于语言（如 Visual C# 和 Visual Basic）的项目类型。 Visual Studio还可以创建自己的项目类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project types, adding
- projects [Visual Studio SDK], adding new types
ms.assetid: 263a084f-f97a-4e09-add7-f0e8a6a27daf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b3a4b440b5b9fd446eba226431e5dd88e8074591d6bad12815020cb6cba04edd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401357"
---
# <a name="project-types"></a>项目类型
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 包括多种语言项目类型，如 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 还允许创建自己的项目类型。

## <a name="in-this-section"></a>本节内容
- [概要](../../extensibility/internals/project-type-essentials.md)

 显示开始使用项目类型时必须了解的重要信息。

- [创建项目类型](../../extensibility/internals/creating-project-types.md)

 讨论项目类型的设计。

- [将命令添加到解决方案资源管理器工具栏](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)

 详细说明向工具栏添加按钮时必须遵循 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] **解决方案资源管理器** 步骤。

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)

 讨论如何将模板添加到项目类型，以便用户可以根据模式创建新项目和项目项。

- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)

 提供有关如何管理项目类型支持的项目的信息。

- [管理配置选项](../../extensibility/internals/managing-configuration-options.md)

 讨论项目类型如何支持配置选项，如"调试"和"发布"，这些选项控制项目的生成、调试等方式。

- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)

 提供有关如何将对源代码管理系统的支持添加到项目类型的信息。

- [嵌套项目](../../extensibility/internals/nesting-projects.md)

 说明项目类型如何支持 *嵌套*，以便可以将项目分组到 **解决方案资源管理器。**

- [升级项目](../../extensibility/internals/upgrading-projects.md)

 描述项目类型如何参与升级向导，以从 早期版本升级项目文件 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [体系结构](../../extensibility/internals/project-types-architecture.md)

 提供有关项目类型的详细技术信息。

## <a name="related-sections"></a>相关章节
- [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)

 概述 IDE 集成开发环境 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (IDE) 将项目显示为层次结构。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 提供指向项目子类型主题的链接。 Project子类型允许扩展大多数类型的项目类型，包括你自己的项目类型。

- [项目](../../extensibility/internals/projects.md)

 介绍如何扩展项目 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 系统。
