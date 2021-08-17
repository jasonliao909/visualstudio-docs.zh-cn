---
title: Visual Studio 2019 SDK |Microsoft Docs
description: SDK Visual Studio 2019 Visual Studio新增和更新的功能，包括编辑器注册增强功能。
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

Visual Studio SDK 具有以下适用于 Visual Studio 2019 的新增和更新的功能。

## <a name="synchronously-autoloaded-extensions-warning"></a>同步自动加载扩展警告

如果用户安装的任何扩展在启动时同步自动加载，则用户现在会看到警告。 可以在同步自动加载的扩展 [中了解有关警告的更多信息](synchronously-autoloaded-extensions.md)。

## <a name="single-unified-visual-studio-sdk"></a>单一、统Visual Studio SDK

现在，可以通过单个 Visual Studio包[Microsoft.VisualStudio.SDK](https://www.nuget.org/packages/microsoft.visualstudio.sdk)获取NuGet SDK 资产。

## <a name="editor-registration-enhancements"></a>编辑器注册增强功能

自创建以来，Visual Studio 支持自定义编辑器注册，其中编辑器可以声明其特定扩展（例如 .xaml 和 .rc) ）的关联 (或者它适用于任何扩展 (.*) 。 从 2019 Visual Studio 16.1 开始，我们扩展了对编辑器注册的支持。

### <a name="filenames"></a>文件名

除了注册对特定文件扩展名的支持，编辑器还可以注册它支持特定文件名，具体方法为将新属性应用于编辑器的 `ProvideEditorFilename` 包。

例如，支持所有 .json 文件的编辑器将此属性 `ProvideEditorExtension` 应用于其包：

```cs
[ProvideEditorExtension(typeof(MyEditor), ".json", MyEditor.Priority)]
```

从 16.1 开始，如果 MyEditor 仅支持几个已知的 .json 文件，它可以改为将这些属性应用于 `ProvideEditorFilename` 其包：

```cs
[ProvideEditorFilename(typeof(MyEditor), "particular.json", MyEditor.Priority)]
[ProvideEditorFilename(typeof(MyEditor), "special.json",    MyEditor.Priority)]
```

### <a name="uicontexts"></a>UIContexts

编辑器可以注册一个或多个 UIContext，这些 UIContext 表示启用时。 UIContexts 通过向注册编辑器的包应用 的一 `ProvideEditorUIContextAttribute` 个或多个 实例进行注册。

如果编辑器已注册 UIContexts：

- 如果打开具有给定扩展名的文件时，至少有一个已注册的 UIContext 处于活动状态，编辑器将包含在编辑器搜索中。
- 如果任何已注册的 UIContext 均不处于活动状态，编辑器搜索中不包含编辑器。

如果编辑器未注册任何 UIContext，它始终包含在该扩展的编辑器搜索中。

例如，如果编辑器仅在 C# 项目打开时可用，则可以通过应用属性来声明此 `ProvideEditorUIContext` 关联：

```cs
[ProvideEditorUIContext(typeof(MyEditor), KnownUIContexts.CSharpProjectContext)]
```
