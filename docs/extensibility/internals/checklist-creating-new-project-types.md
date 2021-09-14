---
title: 清单：创建新的Project类型|Microsoft Docs
description: 了解在项目中创建和显示新项目类型时必须完成Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], creating new types
- project types, checklist for creating
ms.assetid: 29eb9c3b-1933-4741-aa85-65a33f0825ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e7cb031b55a83dbc2694b8532c91b013a343ffa3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600872"
---
# <a name="checklist-create-new-project-types"></a>清单：创建新项目类型
必须完成多个任务以创建新项目类型。 以下清单提供了这些任务的指南：

1. 为新项目类型设计功能。 有关详细信息，请参阅Project[设计决策](../../extensibility/internals/project-type-design-decisions.md)。

2. 确定哪些编辑器用于代码和其他项目元素。 可以使用核心编辑器或标准编辑器，也可以创建和使用特定于项目的编辑器。 有关详细信息，请参阅[创建自定义编辑器和设计器和](../../extensibility/creating-custom-editors-and-designers.md)[如何：打开特定于项目的编辑器](../../extensibility/how-to-open-project-specific-editors.md)。

3. 确定项目项在对象浏览器 和 类视图 **中的参与级别**。  有关详细信息，请参阅 [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)。

4. 基于之前为项目和项目项做出的设计决策派生新类。

5. 编写以下项目类型组件的代码：

    - Project工厂，用于管理创建新项目和打开现有项目。 有关详细信息，请参阅 [使用项目工厂 创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)。

    - Project层次结构和命令处理。 有关详细信息，请参阅使用[HierUtil7](/previous-versions/bb166212(v=vs.100))项目类实现项目类型 (C++) 、项目模型的元素[、Project](../../extensibility/internals/project-model-core-components.md)模型核心组件 和[MenuCommands 与 OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015)。 [](../../extensibility/internals/elements-of-a-project-model.md)

    - Project项管理，包括将项目添加到"新建 **Project对话框中。** 有关详细信息，请参阅[添加项目和项目项模板和](../../extensibility/internals/adding-project-and-project-item-templates.md)[注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。

    - 项目状态和单个项的持久性。 有关详细信息，请参阅打开 [并保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。 有关解决方案信息的持久性，请参阅 [解决方案](../../extensibility/internals/solutions-overview.md)。

    - 要显示在配置文件中的与配置属性窗口。 有关详细信息，请参阅扩展 [属性](../../extensibility/internals/extending-properties.md)。

    - Project页中实现的配置属性，以显示与配置相关的属性。 有关详细信息，请参阅管理 [配置选项](../../extensibility/internals/managing-configuration-options.md)。

    - 枚举部署的输出。 有关详细信息，请参阅输出[Project配置](../../extensibility/internals/project-configuration-for-output.md)。

    - Project启动服务。 有关详细信息，请参阅[项目模型的元素和](../../extensibility/internals/elements-of-a-project-model.md)Project[核心组件](../../extensibility/internals/project-model-core-components.md)。

    - 可用于自动化的对象或派生自 `IDispatch` 的类。

    - XML 命令表 (*.vsct*) 文件。 有关详细信息，请参阅命令[Visual Studio表 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

6. 测试、调试和启动项目类型。

7. 将 设置为 的值 **，Project"** 添加引用"对话框的"项目" `VARIANT_TRUE` 选项卡中显示项目 `VSHPROPID_ShowProjInSolutionPage` 。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>。

8. 创建 Microsoft Installer *(.msi)* 安装 VSPackages。 有关详细信息，请参阅使用 Windows 安装程序安装[VSPackage、](../../extensibility/internals/installing-vspackages-with-windows-installer.md)[注册项目类型和](../../extensibility/internals/registering-a-project-type.md) [VSPackage。](../../extensibility/internals/vspackages.md)

## <a name="see-also"></a>另请参阅
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [何时创建项目类型](../../extensibility/internals/when-to-create-project-types.md)
- [创建项目类型](../../extensibility/internals/creating-project-types.md)