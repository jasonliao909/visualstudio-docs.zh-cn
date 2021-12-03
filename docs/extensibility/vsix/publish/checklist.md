---
title: 最佳做法清单
description: 在发布扩展之前，确保扩展遵循最佳做法的清单。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 7fcdb233f5006a4da2bd647a2ae4113696e51eb5
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515827"
---
# <a name="best-practices-checklist-to-publish-a-visual-studio-extension"></a>发布扩展插件的最佳实践Visual Studio清单

下面是在发布扩展之前，请务必记住Visual Studio列表。

以下视频介绍了最佳做法，以确保扩展是最佳扩展。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWPmjM]

## <a name="adhere-to-threading-rules"></a>遵循线程规则
将[Microsoft.VisualStudio.SDK.Analyzers](https://www.nuget.org/packages/Microsoft.VisualStudio.SDK.Analyzers/) NuGet 包添加到 VSIX 项目，这将帮助你发现和解决线程处理最佳做法的常见冲突。

## <a name="add-high-quality-icon"></a>添加高质量图标
所有扩展都应具有与之关联的图标。 请确保该图标是一个高质量的.png文件，其大小为 **90x90** 像素（96 DPI 或更高）。 将图标添加到 VSIX 项目后，在 **.vsixmanifest** 文件中注册它作为图标和预览图像。

## <a name="name-and-description"></a>名称和说明
研究表明，具有简短且描述性名称和准确说明的扩展更有可能由用户安装。 请确保该名称反映扩展功能的本质。 **.vsixmanifest** 文件的简短说明应设置扩展功能的预期。 因此，简要提及它解决了哪些问题，以及它的主要功能是关键。

## <a name="write-good-marketplace-description"></a>编写良好的市场说明
这是使扩展成功应执行的重要操作之一。 好的说明包括：

* 扩展添加的 UI 的屏幕截图/动画 GIF。
* 各个功能的详细说明。
* 指向更多详细信息的链接（如果适用）。

## <a name="add-license"></a>添加许可证
此许可证将显示在市场、VSIX 安装程序以及"扩展和更新 **..."** 对话框中。 应始终指定许可证以设置用户的预期。 使用 [choosealicense.com](https://choosealicense.com/) 帮助查找适当的许可证。 许可证对于帮助消除任何问题和歧义非常重要，这一点对于许多用户Visual Studio很重要。

## <a name="add-privacy-notice"></a>添加隐私声明
如果扩展收集数据（如遥测数据或以任何其他方式与远程终结点通信）时，请添加说明中的相关说明。

## <a name="use-knownmonikers-when-possible"></a>尽可能使用 KnownMonikers
Visual Studio [KnownMonikers](../../image-service-and-catalog.md)集合中提供了数千个图标。 将图标添加到命令按钮时，请参阅能否使用现有的 KnownMonikers 图标，因为它们是用户熟悉的设计Visual Studio一部分。 下面是 [KnownMonikers](http://glyphlist.azurewebsites.net/knownmonikers/) 的完整列表，并获取 [KnownMonikers Explorer](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.knownmonikersexplorer) 扩展，找到适合你的方案的扩展。

## <a name="make-it-feel-native-to-vs"></a>使其感觉对 VS 是本机的
遵循用户本身使用的相同Visual Studio和原则，使扩展让用户感觉自然。 它还减少了设计不佳的 UI 导致的干扰。 请确保所有按钮、菜单、工具栏和工具窗口在默认情况下仅在用户位于正确的上下文中才能使用它们时可见。 需要遵循一些经验法则：

* 请勿在"文件"、"编辑"和"... ("旁边添加新的) 。
* 按钮、菜单和工具栏不应在它们不适用于的上下文中可见。
* 如果需要 [自动](https://github.com/microsoft/VSSDK-Extensibility-Samples/tree/master/AsyncPackageMigration) 加载 (它可能不会) ，请尽可能晚地执行。
* 使用 [VisibilityConstraints](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/VisibilityConstraints) 切换命令的可见性，而不是依赖于自动加载。

## <a name="use-proper-version-ranges"></a>使用正确的版本范围
支持 2010 Visual Studio版本可能很Visual Studio，以确保每个人都可以使用新的扩展。 问题在于，通过这样做，不再能够使用扩展支持的最低版本之后引入的任何 API。 通常，这些新 API 非常重要，有助于提高扩展以及扩展本身Visual Studio和可靠性。

下面是建议确定要支持Visual Studio版本：

* 仅支持旧版和当前Visual Studio版本 - 如果可能，不支持旧版本。
* 不要指定开放式版本范围，例如 `[16.0,)` 。 详细了解版本 [范围](https://devblogs.microsoft.com/visualstudio/visual-studio-extensions-and-version-ranges-demystified/)。