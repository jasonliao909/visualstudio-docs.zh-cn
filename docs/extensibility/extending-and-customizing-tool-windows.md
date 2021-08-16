---
title: 扩展和自定义工具Windows |Microsoft Docs
description: 了解如何扩展和自定义 Visual Studio提供的工具窗口，包括属性窗口、输出窗口和任务列表窗口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, essentials
- tool windows, standard
ms.assetid: 46b2892e-7b2b-4b3f-83a7-b884f1e114ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4b09b0101e7bcab1f342a214d4585e9b54979e099decf3295d705a10a68fc1da
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432899"
---
# <a name="extend-and-customize-tool-windows"></a>扩展和自定义工具窗口
Visual Studio提供了几种不同类型的窗口，例如工具窗口、文档窗口和对话框窗口。 其他窗口（如" **属性"** 窗口 **、"输出** "窗口和 **任务列表窗口）** 是工具窗口的类型。

## <a name="tool-windows"></a>工具窗口
 Visual Studio工具窗口通常是非基于文件的只读窗口。 在这方面，它们不同于文档窗口，文档窗口在读写模式下显示文件。 工具窗口的示例包括“工具箱” 、“解决方案资源管理器” 、“属性”  窗口和“Web 浏览器”  。

 若要了解如何创建简单的工具窗口，请参阅 [添加工具窗口](../extensibility/adding-a-tool-window.md)。

 若要向工具窗口注册Visual Studio，请参阅[注册工具窗口](../extensibility/registering-a-tool-window.md)。

 工具窗口默认情况下是单实例，这意味着一次只能打开一个工具窗口的实例。 打开单实例工具窗口后，它保持打开状态直到关闭 IDE。 关闭单实例工具窗口时，仅更改其可见性。 你还可以创建多实例工具窗口，以便可以同时打开窗口中的多个实例。 有关详细信息 [，请参阅创建多](../extensibility/creating-a-multi-instance-tool-window.md) 实例工具窗口。

 工具窗口可以是 *动态* 的 ，这意味着每当应用其相关 UI 上下文时，窗口都可见。 使用自动可见性可以减少 IDE 中的窗口的混乱。 有关详细信息，请参阅 [打开动态工具窗口](../extensibility/opening-a-dynamic-tool-window.md)。

 工具窗口可以在文档框架中停靠、浮动或呈选项卡式。 工具窗口框架由 IDE 提供，用于控制大小、位置、停靠状态和其他持久性属性。 工具窗口窗格用于显示内容。 仅当首次打开工具窗口时才应用默认大小和位置；在此之后将保留工具窗口状态。

 工具窗口窗格可以承载 WPF 用户控件，并支持工具栏。 你可以重写 <xref:Microsoft.VisualStudio.Shell.WindowPane.Window%2A> 属性以返回所承载的控件的句柄。

 可以将许多不同的功能添加到工具窗口。 例如，可以添加工具栏 [：向](../extensibility/adding-a-toolbar-to-a-tool-window.md) 工具窗口或快捷菜单添加工具栏 [：在工具窗口中添加快捷菜单](../extensibility/adding-a-shortcut-menu-in-a-tool-window.md)。 可以添加"搜索"控件，用于搜索工具窗口中的项： [将搜索添加到工具窗口](../extensibility/adding-search-to-a-tool-window.md)。

 可以订阅工具窗口事件： [订阅事件](../extensibility/subscribing-to-an-event.md)。

## <a name="extend-existing-tool-windows"></a>扩展现有工具窗口
 可以将有关工具窗口的信息添加到新的"选项"页和"属性"页上的新设置，并写入任务列表 **和输出** 窗口。 有关详细信息，请参阅扩展 [属性、任务列表、输出和选项窗口](../extensibility/extending-the-properties-task-list-output-and-options-windows.md)。

## <a name="modal-dialog-boxes"></a>模式对话框
 在Visual Studio扩展中，应该通过从 派生模式对话框来创建这些对话框，这样就可以控制这些对话框和 <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow?displayProperty=fullName> UI 的其余部分。 有关详细信息，请参阅 [创建和管理模式对话框](../extensibility/creating-and-managing-modal-dialog-boxes.md)。

## <a name="see-also"></a>另请参阅
- [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)
- [扩展项目](../extensibility/extending-projects.md)
- [扩展解决方案](../extensibility/extending-solutions.md)
