---
title: 创建 Project 类型 |Microsoft Docs
description: 了解如何通过设计、创建和注册支持编程任务的新项目类型来扩展 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, new
- projects [Visual Studio SDK], new project types
ms.assetid: bdb2d22e-d622-450c-bb2d-98152a745fcf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f4728412127311475b7861a2640ef96ac55f94387e79357a6bbee0a5c3fa0f01
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448152"
---
# <a name="create-project-types"></a>创建项目类型
可以 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 通过创建新的项目类型来扩展。 若要创建新的项目类型，您必须了解若干概念并完成多个步骤。 以下主题概述了如何创建项目类型。

## <a name="in-this-section"></a>本节内容
- [Project 类型设计决策](../../extensibility/internals/project-type-design-decisions.md)

 讨论了在创建新的项目类型之前必须做出的项目、项目文件持久性和承诺 mechanic 设计决策。

- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)

 概述创建新的项目类型时必须遵循的步骤，该类型支持在项目中编辑代码和编译、构建、调试和部署应用程序的编程任务。

- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)

 提供有关如何提供和使用项目工厂来创建新项目实例的信息。

- [注册项目类型](../../extensibility/internals/registering-a-project-type.md)

 提供注册表中提供默认路径和数据的语句的代码示例，以及包含每个语句的注册表脚本项的表。

- [Project 持久性](../../extensibility/internals/project-persistence.md)

 讨论 `IPersistFileFormat` 如何使用来持久保存文件和非基于文件的项目对象。

- [使用 MSBuild](../../extensibility/internals/using-msbuild.md)

 描述您的项目类型如何使用 [!INCLUDE[vstecmsbuild](../../extensibility/internals/includes/vstecmsbuild_md.md)] 生成引擎使用户能够在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 命令行中生成。

## <a name="related-sections"></a>相关章节
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 介绍代码查看工具的体系结构，例如 **对象浏览器** 和 **类视图** 窗口。 介绍用于在 VSPackage 中实现对象浏览的接口和方法。

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)

 讨论项目在确定项目项打开时使用的编辑器，以及如何操作项目资源的重要性。

- [安装 vspackage 与 Windows Installer](../../extensibility/internals/installing-vspackages-with-windows-installer.md)

 说明如何为 VSPackage 提供自己唯一的标识，以及如何将 VSPackage dll 和其他信息包装到 Windows Installer 包中 (*.MSI* 文件) 部署到客户。

- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)

 说明如何 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 查看和寻址层次结构。

- [VSPackages](../../extensibility/internals/vspackages.md)

 概述 VSPackage，它是一个可安装的 COM 对象，可用于扩展 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 环境并讨论如何实现您自己的 VSPackage。

- [项目类型](../../extensibility/internals/project-types.md)

 讨论如何使用项目来修改代码、编译和生成代码，以及运行和调试代码，并提供指向有关如何创建项目类型的详细主题的链接。
