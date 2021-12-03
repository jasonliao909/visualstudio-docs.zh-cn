---
title: 有用的资源
description: 有助于更好地导航 VS 扩展性的世界的方便资源列表。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 713a9e90a5bee2966699db4c53ea7156472852c1
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515820"
---
# <a name="useful-resources-on-visual-studio-extensions"></a>Visual Studio 扩展上有用的资源

这些资源可帮助你更好地浏览 Visual Studio 扩展性的世界。

以下视频为 Visual Studio 扩展作者引入有用资源。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWP8Kw]

## <a name="resources"></a>资源
下面是一些有用的资源，可帮助你扩展扩展。

* [GitHub 上的 VSIX Community](https://github.com/VsixCommunity)
* [VSIX Community 示例存储库](https://github.com/VsixCommunity/Samples)
* [官方 VS SDK 文档](../../index.yml)
* [VS SDK 示例存储库](https://github.com/Microsoft/VSSDK-Extensibility-Samples)
* [Gitter.im 上的扩展性 chatroom](https://gitter.im/Microsoft/extendvs)

## <a name="know-how-to-search-for-help"></a>了解如何搜索帮助
写入扩展是一种小规模活动，因此搜索联机帮助不会始终返回相关结果。 不过，可以通过多种方式优化搜索词，从而生成更好的结果。

* 使用精确的接口和类名称作为搜索词的一部分。
* 尝试将 " *VSIX*"、" *VSSDK* " 或 " *Visual Studio* " 添加到搜索词。
* 如果可能，请直接搜索 GitHub 而不是 Google/必应。
* 向 [Gitter.im](https://gitter.im/Microsoft/extendvs) chatroom 上的其他扩展器提出问题。

## <a name="use-open-source-as-a-learning-tool"></a>使用开源作为学习工具
您可能对希望扩展的功能和工作原理有一些看法。 但你应该使用哪些 Api，以及如何正确地挂钩它？ 这是很难解决的问题，很多人都放弃了。

一种很好的方法是在 Marketplace 中查找执行类似操作的扩展，或使用类似于你想要执行的操作的元素。 然后查找这些扩展的源代码，并查看它们的作用及其使用的 Api，并从那里查看。

## <a name="book"></a>书籍
若要立即开始学习 Visual Studio 扩展性模型，请考虑[Visual Studio 扩展性开发](https://www.amazon.com/Visual-Studio-Extensibility-Development-Productivity/dp/1484258525)书籍，Rishabh Verma。

:::image type="content" source="../media/book.png" alt-text="Visual Studio 扩展性开发手册。":::

这是可从中了解的最佳书籍。

## <a name="glossary"></a>术语表
为了更好地理解此社区工具包并能够联机搜索帮助，有一个可扩展性术语共享词汇非常重要。 下面是一个按字母顺序排列的概念列表，这些概念和字词对于扩展器有所了解。

### <a name="dte"></a>DTE
*EnvDTE 是一个程序集包装的 COM 库，其中包含 Visual Studio 核心自动化的对象和成员*。 或者是一个易于使用的界面，用于与 Visual Studio 进行交互。

### <a name="marketplace"></a>市场
[Visual Studio Marketplace](https://marketplace.visualstudio.com)是扩展器用于与全球共享扩展的公共扩展存储。 它由 Microsoft 拥有和维护，并且是唯一的官方扩展 marketplace。

### <a name="mef"></a>MEF
Managed Extensibility Framework 由 Visual Studio 中的多个组件使用。 它是注册扩展点的另一种方式，而不是 *包*。

### <a name="package"></a>包
有时称为 *包类*。 `InitializeAsync(...)`Visual Studio 调用其方法来初始化扩展。 从这里，你添加了事件侦听器并注册了命令、工具窗口、设置和其他内容。 在编译期间， *包类* 的属性用于生成一个 .pkgdef 文件，该文件将自动添加到扩展中。

### <a name="pkgdef"></a>.pkgdef
这是一个包，其中包含要添加到 Visual Studio 的私有注册表中的键和值。 可以从包类自动生成此文件，也可以手动创建 .pkgdef 文件，并 `<Asset>` 在 source.extension.vsixmanifest 文件中将其包含为。

### <a name="vsct"></a>.VSCT
Visual Studio 命令表文件。 这是声明菜单、命令和键绑定的位置。

### <a name="vsix"></a>VSIX
指的是 Visual Studio 扩展的文件扩展名 ( .vsix) ，并同时作为 Visual Studio 扩展性的伪。

### <a name="vssdk"></a>VSSDK
这是 *Visual Studio SDK* 的简称，这是构成公共表面的类、服务和组件都是 Visual Studio 的扩展性 API。 通常在引用[VisualStudio](https://www.nuget.org/packages/Microsoft.VisualStudio.SDK/) NuGet 包时使用。

在[Visual Studio SDK 术语表](../../visual-studio-sdk-glossary.md)中查找详细信息。
