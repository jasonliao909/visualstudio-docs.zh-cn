---
title: 设置 Visual Studio 深色主题并更改文本颜色
description: 了解如何在代码编辑器中将默认 Visual Studio 颜色主题更改为深色模式，以及如何更改字体颜色。
ms.date: 11/24/2021
ms.topic: how-to
ms.custom: contperf-fy21q1
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 175b1ca7fc4bbe5194734d36e777a99a2c4c9e65
ms.sourcegitcommit: 3972b1af15930a73d79482e798154f0417a68593
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/30/2021
ms.locfileid: "135649819"
---
# <a name="how-to-personalize-the-visual-studio-ide-and-the-editor"></a>如何：个性化设置 Visual Studio IDE 和编辑器

::: moniker range="vs-2022"

在本操作指南文章中，我们将自定义 Visual Studio 颜色主题。 然后，介绍如何在代码编辑器中为两种不同类型的文本自定义颜色。

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

## <a name="set-the-color-theme-for-the-ide"></a>设置 IDE 的颜色主题

Visual Studio 用户界面的默认颜色主题是“深色”。 下面介绍如何将其更改为其他颜色主题。

1. 在菜单栏上，选择“工具”>“选项” 。

1. 在选项列表中，选择“环境”>“常规” 。

1. 在 " **颜色主题** " 列表中，选择 "默认 **深色** 主题"、" **蓝色** 主题"、" **蓝色 (额外对比度)** 主题和" **浅色** 主题 "。 或者，选择“使用系统设置”选项选择 Windows 使用的主题。

   :::image type="content" source="media/vs-2022/fonts-colors-theme.png" alt-text="可在其中更改颜色主题的“选项”对话框的屏幕截图。":::

   > [!NOTE]
   > 当你更改颜色主题时，IDE 中的文本将恢复为默认值，或恢复为之前为该主题自定义的字体和大小。

    > [!TIP]
    > 想要更多的主题选项？ 在 [Visual Studio Marketplace](https://marketplace.visualstudio.com/search?target=VS&category=Tools&vsVersion=&subCategory=Themes&sortBy=Installs) 上查看各种自定义主题。 若要查看基于 VS Code 的新的 Visual Studio 2022 自定义主题的示例，请参阅[新的 Visual Studio 主题集合简介](https://devblogs.microsoft.com/visualstudio/custom-themes/)博客文章。

::: moniker-end

::: moniker range="vs-2019"

本操作指南文章介绍了如何将 Visual Studio 颜色主题从蓝色主题自定义为深色主题。 然后，介绍如何在代码编辑器中为两种不同类型的文本自定义颜色。

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

## <a name="set-the-color-theme-for-the-ide"></a>设置 IDE 的颜色主题

Visual Studio 用户界面的默认颜色主题是“蓝色”。 让我们将其更改为“深色”  。

1. 在菜单栏上，这是“文件”和“编辑”等菜单的行，选择“工具”>“选项”   。

1. 在“环境”>“常规”选项页上，将“颜色主题”选择内容更改为“深色”，然后选择“确定”    。

   将整个 Visual Studio 开发环境 (IDE) 的颜色主题更改为“深色”  。

   ![深色主题中的 Visual Studio 2019](media/vs-2019/dark-theme.png)

> [!TIP]
> 可以通过从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-madsk.ColorThemeDesigner) 中安装“Visual Studio 颜色主题设计器”  来创建自己的主题。

::: moniker-end

::: moniker range="vs-2017"

本操作指南文章介绍了如何将 Visual Studio 颜色主题从蓝色主题自定义为深色主题。 然后，介绍如何在代码编辑器中为两种不同类型的文本自定义颜色。

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

## <a name="set-the-color-theme-for-the-ide"></a>设置 IDE 的颜色主题

Visual Studio 用户界面的默认颜色主题是“蓝色”。 让我们将其更改为“深色”  。

1. 在菜单栏上，这是“文件”和“编辑”等菜单的行，选择“工具”>“选项”   。

1. 在“环境”>“常规”选项页上，将“颜色主题”选择内容更改为“深色”，然后选择“确定”    。

   将整个 Visual Studio 开发环境 (IDE) 的颜色主题更改为“深色”  。

   ![深色主题中的 Visual Studio 2017](media/quickstart-personalize-dark-theme.png)

> [!TIP]
> 可以通过从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=VisualStudioPlatformTeam.VisualStudio2017ColorThemeEditor) 中安装“Visual Studio 颜色主题编辑器”  来安装其他预定义的主题。 安装此工具后，其他颜色主题将显示在“颜色主题”下拉列表中  。

::: moniker-end

## <a name="change-text-colors-in-the-editor"></a>在编辑器中更改文本颜色

现在我们将为编辑器自定义一些文本颜色。 首先，让我们创建新的 XML 文件来查看默认颜色。

1. 在菜单栏上，选择“文件” > “新建” > “文件”    。

1. 在  “新建文件”对话框的“常规”  类别中，选择“XML 文件”  ，然后选择“打开”  。

1. 将以下 XML 粘贴到包含 `<?xml version="1.0" encoding="utf-8"?>` 的行的下面。

   ```xml
   <Catalog>
     <Book id="bk101">
     <Author>Garghentini, Davide</Author>
     <Title>XML Developer's Guide</Title>
     <Genre>Computer</Genre>
     <Price>44.95</Price>
     <PublishDate>2000-10-01</PublishDate>
     <Description>
       An in-depth look at creating applications with XML.
     </Description>
   </Book>
   <Book id="bk102">
     <Author>Garcia, Debra</Author>
     <Title>Midnight Rain</Title>
     <Genre>Fantasy</Genre>
     <Price>5.95</Price>
     <PublishDate>2000-12-16</PublishDate>
     <Description>
       A former architect battles corporate zombies, an evil
       sorceress, and her own childhood to become queen of the world.
     </Description>
   </Book>
   </Catalog>
   ```

   请注意，行号是翠蓝色，XML 属性（例如 `id="bk101"`）是浅蓝色。 我们将更改这些项的文本颜色。

   ![XML 文件字体颜色](media/quickstart-personalize-xml-file.png)

1. 若要打开“选项”对话框，请在菜单栏中选择“工具” > “选项”    。

1. 在“环境”下  ，请选择  “字体和颜色”类别。

   请注意，“显示以下对象的设置”下的文本显示的是“文本编辑器”   &mdash;这正是我们所需要的。 展开下拉列表，仅查看可用于自定义字体和文本颜色的位置的扩展列表。

1. 若要更改行号文本的颜色，请在“显示项目”  列表中选择“行号”  。 在“项目前景色”  框中，选择“橄榄色”  。

    :::image type="content" source="media/vs-2022/personalize-line-number-color.png" alt-text="“选项”对话框中“字体和颜色”类别的屏幕截图。":::

   某些语言有自己特定的字体和颜色设置。 如果你是 C++ 开发者，且想要更改函数的颜色，则可在“显示项”列表中查找“C++ 函数”   。

1. 退出对话框中之前，让我们同时更改一下 XML 属性的颜色。 在  “显示项”列表中，向下滚动到  “XML 属性”，然后选择它。 在“项目前景色”  框中，选择“浅绿色”  。 选择“确定”以保存我们的选择并关闭对话框。 

   行号现在为橄榄色，XML 属性为明亮的浅绿色。 如果打开另一个类型的文件，例如 C++ 或 C# 代码文件，则会发现行号也以橄榄色显示。

   ![使用新的字体颜色的 XML 文件](media/quickstart-personalize-xml-file-new-colors.png)

我们探讨了几种在 Visual Studio 中自定义颜色的方法。 建议继续深入了解[“选项”](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)对话框中的其他自定义选项，以真正使 Visual Studio 为你所用。

## <a name="see-also"></a>另请参阅

- [如何：在 Visual Studio 中更改字体、颜色和主题](../ide/how-to-change-fonts-and-colors-in-visual-studio.md)
- [如何：在编辑器中更改文本大小写](../ide/how-to-change-text-case-in-the-editor.md)
- [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)
