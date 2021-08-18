---
title: 语言服务和编辑器扩展入门
description: 了解如何将语言服务功能添加到任何内容类型，以及如何自定义 Visual Studio 编辑器的外观和行为。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 6b151891-c06d-40b1-9867-42298caa8492
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6ec5af209d9dc5c28c1c741058502b5be1b44000
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087153"
---
# <a name="get-started-with-language-service-and-editor-extensions"></a>语言服务和编辑器扩展入门

您可以使用编辑器扩展向您自己的编程语言或任何内容类型添加语言服务功能，例如大纲显示、大括号匹配、IntelliSense 和 light 电灯泡。 还可以自定义 Visual Studio 编辑器的外观和行为，例如文本着色、边距、修饰和其他视觉对象。 您还可以定义自己的内容类型，并指定显示内容的文本视图的外观和行为。

 若要开始编写编辑器扩展，请使用作为 Visual Studio SDK 的一部分安装的编辑器项目模板。 Visual Studio SDK 是一组可下载的工具，通过使用 vspackage 或使用 Managed Extensibility Framework (MEF) 来更轻松地开发 Visual Studio 扩展。

> [!NOTE]
> 有关 Visual Studio sdk 的详细信息，请参阅[Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

 建议你在编写自己的编辑器扩展之前了解以下概念和技术。

## <a name="the-windows-presentation-foundation-wpf-and-editor-extensions"></a>WPF) 和编辑器扩展 (Windows Presentation Foundation

 Visual Studio 编辑器用户界面 (UI) 是使用 Windows Presentation Foundation (WPF) 实现的。 WPF 提供丰富的视觉体验和一致的编程模型，该模型将代码的视觉方面与业务逻辑分离。 创建编辑器扩展时，可以使用很多 WPF 元素和功能。 有关详细信息，请参阅[Windows Presentation Foundation](/dotnet/framework/wpf/index)。

## <a name="the-managed-extensibility-framework-mef-and-editor-extensions"></a>MEF) 和编辑器扩展 (Managed Extensibility Framework

 Visual Studio 编辑器使用 Managed Extensibility Framework (MEF) 来管理其组件和扩展。 MEF 还使开发人员可以更轻松地为主机应用程序创建扩展，如 Visual Studio。 在此框架中，根据 MEF 协定定义扩展并将其导出为 MEF 组件部件。 主机应用程序通过查找组件部分来管理这些组件，并对其进行注册，并确保将它们应用到正确的上下文。

> [!NOTE]
> 有关编辑器中的 MEF 的详细信息，请参阅[编辑器中的 Managed Extensibility Framework](../extensibility/managed-extensibility-framework-in-the-editor.md)。

## <a name="visual-studio-editor-extension-points-and-extensions"></a>Visual Studio 编辑器扩展点和扩展

 编辑器扩展点是可以自定义和扩展的 MEF 组件部件。 在某些情况下，通过实现接口并将其与正确的元数据一起导出来扩展扩展点。 在其他情况下，只需声明一个扩展并将其导出为特定类型。

 下面是一些基本类型的编辑器扩展：

- 边距和滚动条

- Tags

- 修饰

- 选项

- IntelliSense

  有关编辑器扩展点的详细信息，请参阅 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)。

## <a name="deploying-editor-extensions"></a>部署编辑器扩展

 在 Visual Studio 中，你将通过将名为 source.extension.vsixmanifest 的元数据文件添加到解决方案中，生成解决方案，然后将二进制文件和清单的副本添加到已知 Visual Studio 的文件夹中来部署编辑器扩展 *。* 清单文件定义有关扩展的基本事实 (例如，名称、作者、版本和内容) 类型。 有关 VSIX 清单文件和如何部署扩展的详细信息，请参阅[发运 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。

 在计算机上安装扩展时，请将二进制文件和清单包含在 Visual Studio 已知的文件夹的子文件夹中。

> [!WARNING]
> 如果使用 Visual Studio 中包含的某个编辑器扩展性模板，则无需担心清单和部署位置的详细信息。 这些模板包含注册和部署扩展所需的所有内容。

## <a name="run-extensions-in-the-experimental-instance"></a>在实验实例中运行扩展

 在开发扩展时，可以将 Visual Studio 的工作版本隔离，方法是在 Windows Vista 上的以下试验文件夹 (中部署扩展，并 Windows 7) ：

 *{% LOCALAPPDATA%} \VisualStudio\10.0Exp\Extensions \\ {Company} \\ {ExtensionID}*

 其中， *% LOCALAPPDATA%* 是登录用户的名称， *company* 是拥有该扩展的公司的名称， *ExtensionID* 是扩展的 ID。

 将扩展部署到实验位置时，它将在调试模式下运行。 将启动 Visual Studio 的第二个实例，并将其命名为 **Microsoft Visual Studio 实验实例**。

## <a name="manage-extensions"></a>管理扩展

 "**工具**" 菜单上的 "**扩展和更新**" (中列出了 Visual Studio 的扩展) 。 如果在实验实例中测试扩展，则该扩展将列在实验实例中的 " **扩展和更新** " 中，但不会在开发实例中列出。

 有关详细信息，请参阅[查找和使用 Visual Studio 扩展](../ide/finding-and-using-visual-studio-extensions.md)。

## <a name="use-templates-to-create-editor-extensions"></a>使用模板创建编辑器扩展

 可以使用编辑器模板创建自定义分类器、修饰和边距的 MEF 扩展。 c # 和 Visual Basic 项目都有模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

 你还可以使用 VSIX Project 模板来创建扩展。 此模板仅提供部署任何类型的扩展所需的元素，并包括 *source.extension.vsixmanifest* 文件、所需的程序集引用和包含允许你部署扩展的生成任务的项目文件。 有关详细信息，请参阅 [VSIX 项目模板](../extensibility/vsix-project-template.md)。

 你还可以从 Visual Studio 包扩展中创建编辑器 MEF 组件。 有关详细信息，请参阅以下演练：

- [演练：在编辑器扩展中使用 shell 命令](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)

- [演练：在编辑器扩展中使用快捷键](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)

## <a name="see-also"></a>另请参阅

- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
