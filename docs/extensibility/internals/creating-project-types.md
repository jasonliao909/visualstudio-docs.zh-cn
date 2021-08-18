---
title: 创建Project类型|Microsoft Docs
description: 了解如何通过Visual Studio、创建和注册支持编程任务的新项目类型来扩展应用程序。
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
可以通过创建新 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目类型进行扩展。 若要创建新项目类型，必须了解多个概念并完成多个步骤。 以下主题概述了如何创建项目类型。

## <a name="in-this-section"></a>本节内容
- [Project类型设计决策](../../extensibility/internals/project-type-design-decisions.md)

 讨论在创建新项目类型之前必须做出的项目、项目文件持久性和承诺型设计决策。

- [清单：创建新项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)

 概述创建新项目类型时必须执行的步骤，此类项目类型支持编辑代码和在项目中编译、生成、调试和部署应用程序等编程任务。

- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)

 提供有关如何提供和使用项目工厂来创建新项目实例的信息。

- [注册项目类型](../../extensibility/internals/registering-a-project-type.md)

 提供注册表中提供默认路径和数据的 语句的代码示例，以及包含每个语句的注册表脚本条目的表。

- [Project持久性](../../extensibility/internals/project-persistence.md)

 讨论如何使用 来 `IPersistFileFormat` 持久保存文件对象和非基于文件的项目对象。

- [使用 MSBuild](../../extensibility/internals/using-msbuild.md)

 描述项目类型如何使用生成 [!INCLUDE[vstecmsbuild](../../extensibility/internals/includes/vstecmsbuild_md.md)] 引擎让用户在命令行和 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 命令行中生成。

## <a name="related-sections"></a>相关章节
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)

 介绍代码查看工具的体系结构，如 **对象浏览器** 和 **类视图窗口。** 介绍用于在 VSPackage 中实现对象浏览的接口和方法。

- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)

 讨论项目在确定打开项目项时使用哪个编辑器以及如何处理项目资源方面的重要性。

- [使用安装程序安装 VSPackage Windows](../../extensibility/internals/installing-vspackages-with-windows-installer.md)

 演示如何为 VSPackage 提供自己的唯一标识，以及如何将 VSPackage DLL 和其他信息包装在 Windows Installer 包 (*.MSI* 文件中) 以部署到客户。

- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)

 描述 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 视图和地址层次结构。

- [VSPackages](../../extensibility/internals/vspackages.md)

 概述 VSPackage，这是一个可安装的 COM 对象，可扩展环境并讨论如何 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 实现自己的 VSPackage。

- [项目类型](../../extensibility/internals/project-types.md)

 讨论如何使用项目来修改代码、编译和生成代码以及运行和调试代码，并提供指向如何创建项目类型的详细主题的链接。
