---
title: 语言服务和编辑器扩展入门
description: 了解如何将语言服务功能添加到任何内容类型，以及如何自定义文本编辑器Visual Studio行为。
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
ms.openlocfilehash: b9518179b0096dcb7527ea5e9eba4e72cbc70727c7d6f73af4b59f6cb22d08cc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359970"
---
# <a name="get-started-with-language-service-and-editor-extensions"></a>语言服务和编辑器扩展入门

可以使用编辑器扩展将语言服务功能（如大纲显示、大括号匹配、IntelliSense 和灯泡）添加到自己的编程语言或任何内容类型。 还可以自定义编辑器的外观Visual Studio，例如文本着色、边距、装饰和其他可视元素。 还可以定义自己的内容类型，并指定显示内容的文本视图的外观和行为。

 若要开始编写编辑器扩展，请使用作为 Visual Studio SDK 的一部分安装的编辑器项目模板。 Visual Studio SDK 是一组可下载的工具，使用 VSPackage 或 MANAGED EXTENSIBILITY FRAMEWORK (MEF) ，可以更轻松地开发 Visual Studio 扩展。

> [!NOTE]
> 有关此 SDK Visual Studio，请参阅 Visual Studio [SDK。](../extensibility/visual-studio-sdk.md)

 建议在编写自己的编辑器扩展之前了解以下概念和技术。

## <a name="the-windows-presentation-foundation-wpf-and-editor-extensions"></a>WPF Windows Presentation Foundation (和) 扩展

 使用 Visual Studio WPF (实现) UI Windows Presentation Foundation (编辑器) 。 WPF 提供丰富的视觉体验和一致的编程模型，将代码的可视方面与业务逻辑分开。 创建编辑器扩展时，可以使用许多 WPF 元素和功能。 有关详细信息，请参阅[Windows Presentation Foundation。](/dotnet/framework/wpf/index)

## <a name="the-managed-extensibility-framework-mef-and-editor-extensions"></a>MANAGED EXTENSIBILITY FRAMEWORK (MEF) 编辑器扩展

 该Visual Studio编辑器使用 Managed Extensibility Framework (MEF) 来管理其组件和扩展。 MEF 还使开发人员能够更轻松地为主机应用程序（如 Visual Studio） 创建扩展。 在此框架中，根据 MEF 协定定义扩展，并导出为 MEF 组件部件。 主机应用程序通过查找组件部件、注册组件并确保它们应用于正确的上下文来管理组件部件。

> [!NOTE]
> 有关编辑器中 MEF 的信息，请参阅Managed Extensibility Framework[中的设置](../extensibility/managed-extensibility-framework-in-the-editor.md)。

## <a name="visual-studio-editor-extension-points-and-extensions"></a>Visual Studio编辑器扩展点和扩展

 编辑器扩展点是可以自定义和扩展的 MEF 组件部件。 在某些情况下，通过实现 接口并连同正确的元数据一起导出扩展点来扩展扩展点。 在其他情况下，只需声明扩展，并导出为特定类型。

 下面是一些基本类型的编辑器扩展：

- 边距和滚动条

- 标记

- 装饰品

- 选项

- IntelliSense

  有关编辑器扩展点的信息，请参阅 [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)。

## <a name="deploying-editor-extensions"></a>部署编辑器扩展

 在 Visual Studio 中，通过将名为 *source.extension.vsixmanifest* 的元数据文件添加到解决方案、生成解决方案，然后在已知 Visual Studio 的文件夹中添加二进制文件和清单的副本来部署编辑器扩展。 清单文件定义了有关扩展插件的基本 (例如，名称、作者、版本和内容) 。 有关 VSIX 清单文件以及如何部署扩展的信息，请参阅 Ship [Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。

 在计算机上安装扩展时，将二进制文件和清单包括在已知要安装的文件夹的子文件夹中Visual Studio。

> [!WARNING]
> 如果使用包含在清单和部署位置中的编辑器扩展性模板之一，则无需担心清单和部署Visual Studio。 模板包含注册和部署扩展所需的一切内容。

## <a name="run-extensions-in-the-experimental-instance"></a>在实验实例中运行扩展

 在开发扩展时，Visual Studio在 Windows Vista 上的以下实验性文件夹 (和 Windows 7 中部署扩展) ：

 *{%LOCALAPPDATA%}\VisualStudio\10.0Exp\Extensions \\ {Company} \\ {ExtensionID}*

 其中 *%LOCALAPPDATA%* 是登录用户的名称 *，Company* 是拥有扩展的公司的名称 *，ExtensionID* 是扩展的 ID。

 将扩展部署到实验性位置时，它将在调试模式下运行。 启动第二Visual Studio实例，并命名为 **Microsoft Visual Studio - 实验实例**。

## <a name="manage-extensions"></a>管理扩展

 "工具"Visual Studio上的"扩展和更新" (**列出了扩展**) 。 如果在实验实例中测试扩展，该扩展将列在实验实例的"扩展和更新"中，但不在开发实例中列出。

 有关详细信息，请参阅[查找和使用Visual Studio扩展](../ide/finding-and-using-visual-studio-extensions.md)。

## <a name="use-templates-to-create-editor-extensions"></a>使用模板创建编辑器扩展

 可以使用编辑器模板创建用于自定义分类器、装饰和边距的 MEF 扩展。 C# 和项目Visual Basic模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

 还可使用 VSIX Project模板创建扩展。 此模板仅提供部署任何类型的扩展所需的元素，并包括 *source.extension.vsixmanifest* 文件、所需的程序集引用以及包含生成任务的项目文件，以便你能够部署扩展。 有关详细信息，请参阅 [VSIX 项目模板](../extensibility/vsix-project-template.md)。

 还可以从包扩展创建Visual Studio MEF 组件。 有关详细信息，请参阅以下演练：

- [演练：将 shell 命令与编辑器扩展一起使用](../extensibility/walkthrough-using-a-shell-command-with-an-editor-extension.md)

- [演练：将快捷键与编辑器扩展一同使用](../extensibility/walkthrough-using-a-shortcut-key-with-an-editor-extension.md)

## <a name="see-also"></a>另请参阅

- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
