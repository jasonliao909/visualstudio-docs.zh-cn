---
title: Visual Studio 2019 SDK 的新增功能 |Microsoft Docs
description: Visual Studio SDK Visual Studio 2019 的新增功能和更新功能，包括编辑器注册增强功能。
ms.custom: SEO-VS-2020
ms.date: 03/29/2019
ms.topic: conceptual
ms.assetid: 4a07607b-0c87-4866-acd8-6d68358d6a47
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9078b8a6f6150a2ca5f3f6de84bea3facca94073849109f145a7cae64d172039
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121400460"
---
# <a name="whats-new-in-the-visual-studio-2019-sdk"></a>Visual Studio 2019 SDK 的新增功能

Visual Studio SDK 具有适用于 Visual Studio 2019 的下列新增功能和更新功能。

## <a name="synchronously-autoloaded-extensions-warning"></a>同步加载扩展警告

如果任何安装的扩展插件在启动时同步加载，则用户现在会看到警告。 你可以在 [同步加载扩展](synchronously-autoloaded-extensions.md)中了解有关警告的详细信息。

## <a name="single-unified-visual-studio-sdk"></a>单个统一 Visual Studio SDK

现在可以通过单个 NuGet [VisualStudio](https://www.nuget.org/packages/microsoft.visualstudio.sdk)包获取全部 Visual Studio SDK 资产。

## <a name="editor-registration-enhancements"></a>编辑器注册增强功能

自它创建后，Visual Studio 支持自定义编辑器注册，其中编辑器可以为特定扩展声明其相关性 (例如，.xaml 和 .rc) ，或者它适用于任何扩展名 (. * ) 。 从 Visual Studio 2019 版16.1 开始，我们扩大了对编辑器注册的支持。

### <a name="filenames"></a>文件名

除了、或而不是注册特定文件扩展名的支持外，编辑器还可以通过将新属性应用于编辑器的包来注册它是否支持特定文件名 `ProvideEditorFilename` 。

例如，支持所有 json 文件的编辑器会将此 `ProvideEditorExtension` 属性应用到其包：

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

从16.1 开始，如果 MyEditor 仅支持几个已知的 json 文件，则可以将这些 `ProvideEditorFilename` 属性应用到其包：

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>UIContexts

编辑器可以注册一个或多个表示启用时的 UIContexts。 UIContexts 是通过将一个或多个实例应用 `ProvideEditorUIContextAttribute` 于注册编辑器的包来注册的。

如果编辑器已注册 UIContexts：

- 如果打开具有给定扩展名的文件时，其中至少有一个已注册的 UIContexts 处于活动状态，则编辑器将包含在编辑器搜索中。
- 如果没有任何已注册的 UIContexts 处于活动状态，编辑器将不包含在编辑器搜索中。

如果编辑器未注册任何 UIContexts，则它始终包含在编辑器中搜索该扩展插件。

例如，如果编辑器仅在 c # 项目打开时才可用，则它可以通过应用特性来声明此关联 `ProvideEditorUIContext` ：

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
