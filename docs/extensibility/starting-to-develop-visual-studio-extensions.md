---
title: 开始开发 Visual Studio 扩展 |Microsoft Docs
description: 了解第一次开始编写 Visual Studio 扩展时可能会遇到的一些常见问题。
ms.custom: SEO-VS-2020
ms.date: 09/18/2017
ms.topic: conceptual
helpviewer_keywords:
- getting started, Visual Studio integration
- Visual Studio, integration
ms.assetid: 8fe5e2ab-a424-4173-9d39-dd082c4d58d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 260ae4b71d7eb7bed3ac97faa3d0ccf90665f90a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049449"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>开始开发 Visual Studio 扩展

如果你之前从未编写过 Visual Studio 扩展，则可能会遇到一些问题。 这里列出了其中一些最常用的文件。 如果看不到所需的信息，请使用反馈按钮 (**此页面是否有所帮助？** 在屏幕的右上方) ，询问所需内容。

> [!NOTE]
> 本文适用于 Windows 上的 Visual Studio。 有关 Visual Studio for Mac，请参阅[扩展 Visual Studio for Mac](/visualstudio/mac/extending-visual-studio-mac)。 有关 Visual Studio Code，请参阅[Visual Studio Code 扩展 API](https://code.visualstudio.com/api)。

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>开发 Visual Studio 扩展需要什么软件？

除了 Visual Studio 以外，还需要安装 Visual Studio SDK 来开发 Visual Studio 扩展。 你可以将 Visual Studio SDK 作为常规安装程序的一部分进行安装，也可以在以后安装它。 有关安装 Visual Studio sdk 的详细信息，请参阅[安装 Visual Studio sdk](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>Visual Studio 扩展可以执行哪些操作？

当涉及到应该构想不同 Visual Studio 扩展时，天空的限制。 当然，大多数扩展都与编写代码有关，但这不是必须的。 下面是可以生成的扩展类型的一些示例：

- 支持未包含在 Visual Studio 中的语言、语法着色、IntelliSense 以及编译器和调试支持

- 利用附加模板、代码重构、新对话框或工具窗口扩展核心 IDE 体验的生产力工具

- 适用于各种方案（如数据设计或云支持）的域特定设计器

有关扩展的示例，请查看[Visual Studio Marketplace](https://marketplace.visualstudio.com/vs)。 许多扩展是开放源代码的，并且 Marketplace 包含指向其 GitHub 存储库的链接。

## <a name="which-visual-studio-features-can-i-extend"></a>可以扩展哪些 Visual Studio 功能？

理论上，你可以只扩展 Visual Studio 的任何部分：菜单、工具栏、命令、窗口、解决方案、项目、编辑器等。

实际上，我们发现大多数人要扩展的功能是命令、菜单和工具栏、windows、IntelliSense 和项目。 下面是相关章节的链接：

- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)：将您自己的项添加到 Visual Studio 菜单和工具栏中。 您可以使用它们来启动新 Visual Studio 功能或您自己的外部帮助程序应用程序。 还可以提供菜单项的自定义快捷方式。

- [扩展和自定义工具 Windows](../extensibility/extending-and-customizing-tool-windows.md)：扩展现有工具窗口或创建自己的工具窗口。 例如，您可以将新属性添加到 **属性**，也可以创建新的工具窗口来添加其他功能。

- [编辑器和语言服务扩展](../extensibility/editor-and-language-service-extensions.md)：将你自己的自定义添加到为 Visual Studio 语言提供的 IntelliSense，或创建对新编程语言的支持。 你可以创建新的语句完成、建议和新的 QuickInfo 工具提示。 对于轻型电灯泡，可以添加重构建议和代码修补程序，以支持新的编程语言。

- [扩展项目](../extensibility/extending-projects.md)

- [扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)

- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)

- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)

- [Visual Studio 独立 Shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

## <a name="what-project-templates-are-provided-by-the-vssdk"></a><a name="BKMK_ProjectTemplate"></a> VSSDK 提供哪些项目模板？
 这两种主要类型的扩展是 Vspackage 和 MEF 扩展。 通常，VSPackage 扩展用于使用或扩展命令、工具窗口和项目的扩展。 MEF 扩展用于扩展或自定义 Visual Studio 编辑器。

 对于 Visual c # 和 Visual Basic 扩展，VSSDK 提供了一个空的 VSIX 项目模板，可将其与创建菜单命令、工具窗口和编辑器扩展的新项模板一起使用。 你还可以使用此模板打包项目模板、代码片段和其他项目，以便将其分发给其他用户。

 对于 c + +，VSPackage 向导提供代码来添加菜单命令、工具窗口和自定义编辑器。

 独立 Shell 模板用于打包 Visual Studio Shell 版本中的扩展，你可以将其作为自己的品牌和分发。 以下主题说明了如何开始每种类型的扩展：

- 菜单命令： [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

- 工具窗口： [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)

- 编辑器扩展： [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- 基本 Vspackage： [使用 VSPackage 创建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)

- vsix 项目模板：[与 VSIX Project 模板入门](../extensibility/getting-started-with-the-vsix-project-template.md)

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>如何实现将我的扩展显示为 Visual Studio？
 获取有关在[Visual Studio 用户体验指南](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)中设计扩展 UI 的极佳技巧。

## <a name="where-can-i-find-examples-of-vssdk-code"></a>在哪里可以找到 VSSDK 代码的示例？
 上一部分中列出的每个链接都具有分步演练，说明如何实现特定功能。 你还可以在 GitHub [Visual Studio 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)中找到开源 VSSDK 示例。

## <a name="how-can-i-distribute-my-extension"></a>如何分发我的扩展？
 你可以在另一台计算机上安装你的扩展，或将其作为 .vsix 文件发送给你的朋友，你可以通过双击该文件进行安装。 可以在[装运 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)中找到有关 VSIX 包的详细信息。

 你还可以在 Visual Studio Marketplace 上发布扩展，使其对大量 Visual Studio 客户可见。 有关将扩展打包到 Marketplace 的示例，请参阅[演练：发布 Visual Studio 扩展](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)。 若要详细了解如何在 Marketplace 上发布内容，请参阅[Visual Studio 的产品和扩展](/azure/devops/extend/overview?view=vsts&preserve-view=true)。

## <a name="see-also"></a>请参阅

- [扩展 Visual Studio for Mac](/visualstudio/mac/extending-visual-studio-mac)
- [扩展 Visual Studio Code](https://code.visualstudio.com/api)