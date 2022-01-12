---
title: 开始开发Visual Studio扩展|Microsoft Docs
description: 了解首次开始编写扩展时可能Visual Studio常见问题。
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
ms.openlocfilehash: 2680cfd241f1b72a34b853eaef2763063a93793e
ms.sourcegitcommit: 3972b1af15930a73d79482e798154f0417a68593
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/30/2021
ms.locfileid: "135649833"
---
# <a name="starting-to-develop-visual-studio-extensions"></a>开始开发 Visual Studio 扩展

如果以前从未编写过Visual Studio扩展，则可能有一些问题。 我们在此处列出了一些最常见的问题。 如果看不到要查找的信息，请使用反馈按钮 (此页面是否有用 **？** 位于屏幕右上角) 询问你想要的内容。

> [!NOTE]
> 本文适用于 Windows 上的 Visual Studio。 有关Visual Studio for Mac，请参阅[扩展 Visual Studio for Mac。](/previous-versions/visualstudio/mac/extending-visual-studio-mac-walkthrough) 有关Visual Studio Code，请参阅 Visual Studio Code[扩展 API。](https://code.visualstudio.com/api)

## <a name="what-software-do-i-need-to-develop-visual-studio-extensions"></a>需要哪些软件来开发Visual Studio扩展？

需要安装 Visual Studio SDK 以及 Visual Studio 才能开发 Visual Studio 扩展。 可以在常规Visual Studio安装 SDK，也可以稍后安装。 若要详细了解如何安装 Visual Studio SDK，请参阅安装 Visual Studio [SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="what-kinds-of-things-can-i-do-with-visual-studio-extensions"></a>可以使用扩展执行哪些Visual Studio操作？

在虚设不同的扩展名时，天Visual Studio限制。 当然，大多数扩展与编写代码有关，但不必如此。 下面是可以构建的扩展类型的一些示例：

- 支持语言中未包含的语言，Visual Studio语法着色、IntelliSense 以及编译器和调试支持

- 通过其他模板、代码重构、新对话框或工具窗口扩展核心 IDE 体验的工作效率工具

- 适用于数据设计或云支持等方案的特定于域的设计器

有关扩展的示例，请查看 Visual Studio[市场](https://marketplace.visualstudio.com/vs)。 许多扩展都是开源的，市场包含指向其GitHub的链接。

## <a name="which-visual-studio-features-can-i-extend"></a>我可以Visual Studio哪些功能？

从理论上讲，你可以只扩展Visual Studio菜单、工具栏、命令、窗口、解决方案、项目、编辑器等。

在实践中，我们发现大多数用户想要扩展的功能包括命令、菜单和工具栏、窗口、IntelliSense 和项目。 下面是指向相关部分的链接：

- [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)：向菜单和工具栏Visual Studio项。 可以使用它们来启动新的Visual Studio或你自己的外部帮助程序应用程序。 还可以为菜单项提供自定义快捷方式。

- [扩展和自定义工具Windows：](../extensibility/extending-and-customizing-tool-windows.md)扩展现有工具窗口或创建自己的工具窗口。 例如，可以将新属性添加到"属性 **"，** 也可以创建新的工具窗口来添加其他功能。

- [编辑器和语言服务扩展](../extensibility/editor-and-language-service-extensions.md)：将你自己的自定义添加到为语言提供的 IntelliSense Visual Studio，或创建对新编程语言的支持。 可以创建新的语句完成、建议和新的 QuickInfo 工具提示。 借助灯泡，可以添加重构建议和代码修补程序以支持新的编程语言。

- [扩展项目](../extensibility/extending-projects.md)

- [扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)

- [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)

- [扩展 Visual Studio 的其他部分](../extensibility/extending-other-parts-of-visual-studio.md)

- [Visual Studio 独立 Shell](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)

## <a name="what-project-templates-are-provided-by-the-vssdk"></a><a name="BKMK_ProjectTemplate"></a> VSSDK 提供哪些项目模板？
 两种主要类型的扩展是 VSPackage 和 MEF 扩展。 通常，VSPackage 扩展用于使用或扩展命令、工具窗口和项目的扩展。 MEF 扩展用于扩展或自定义Visual Studio编辑器。

 对于 Visual C# 和 Visual Basic 扩展，VSSDK 提供了一个空的 VSIX 项目模板，你可以与用于创建菜单命令、工具窗口和编辑器扩展的新项模板一起使用。 还可使用此模板打包项目模板、代码片段和其他项目，以便分发到其他用户。

 对于 C++，VSPackage 向导提供用于添加菜单命令、工具窗口和自定义编辑器的代码。

 独立 Shell 模板用于将扩展打包到 Visual Studio shell 的版本中，你可以将其品牌化并分发为自己的版本。 以下主题将展示如何开始使用每种扩展：

- 菜单命令 [：使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)

- 工具窗口 [：使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)

- 编辑器扩展： [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)

- 基本 VSPackage： [使用 VSPackage 创建扩展](../extensibility/creating-an-extension-with-a-vspackage.md)

- VSIX 项目模板[：入门 VSIX](../extensibility/getting-started-with-the-vsix-project-template.md) Project模板

## <a name="how-do-i-get-my-extension-to-look-like-visual-studio"></a>如何实现扩展看起来就像Visual Studio？
 在用户体验指南 中获取有关为扩展设计 UI [Visual Studio提示](../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)。

## <a name="where-can-i-find-examples-of-vssdk-code"></a>在哪里可以找到 VSSDK 代码的示例？
 上一部分中列出的每个链接都有分步演练，演示了如何实现特定功能。 还可以在示例 上的 GitHub 上Visual Studio [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

## <a name="how-can-i-distribute-my-extension"></a>如何分发扩展？
 可以将扩展安装到另一台计算机，或将其作为 .vsix 文件发送给朋友，通过双击安装该文件。 有关 VSIX 包的更多信息，Visual Studio[扩展。](../extensibility/shipping-visual-studio-extensions.md)

 还可以在 Visual Studio Marketplace 上发布扩展，使其对大量客户Visual Studio可见。 有关将扩展打包到市场的示例，请参阅[演练：](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)发布Visual Studio扩展。 若要详细了解在市场中发布需要执行哪些工作，请参阅适用于[Visual Studio。](/azure/devops/extend/overview?view=vsts&preserve-view=true)

## <a name="see-also"></a>另请参阅

- [扩展 Visual Studio for Mac](/previous-versions/visualstudio/mac/extending-visual-studio-mac-walkthrough)
- [扩展Visual Studio Code](https://code.visualstudio.com/api)
