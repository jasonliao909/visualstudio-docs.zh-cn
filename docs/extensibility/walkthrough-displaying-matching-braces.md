---
title: 演练：显示匹配的大括号 |Microsoft Docs
description: 了解如何在语言上下文中定义大括号，并使用此演练将大括号匹配标记应用于文本内容类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e4565e095c6bd8fe26f0bb72bd66d6df935ff16b
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217263"
---
# <a name="walkthrough-display-matching-braces"></a>演练：显示匹配的大括号
通过定义要匹配的大括号来实现基于语言的功能（例如，大括号匹配），并在插入符号位于一个大括号中时向匹配大括号添加文本标记标记。 你可以在语言上下文中定义大括号，定义自己的文件扩展名和内容类型，并将标记应用到该类型，或者将标记应用于现有内容类型 (如 "text" ) 。 下面的演练演示如何将大括号匹配标记应用于 "text" 内容类型。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建 Managed Extensibility Framework (MEF) 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建编辑器分类器项目。 将解决方案命名为 `BraceMatchingTest`。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅 [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="implement-a-brace-matching-tagger"></a>实现括号匹配标记
 若要获取类似于在 Visual Studio 中使用的大括号突出显示效果，可以实现类型的标记 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 。 下面的代码演示如何在任何嵌套级别为大括号对定义标记。 在此示例中，[] 和的大括号对 {} 是在标记构造函数中定义的，但在完整语言实现中，将在语言规范中定义相关的大括号对。

### <a name="to-implement-a-brace-matching-tagger"></a>实现括号匹配标记

1. 添加一个类文件并将其命名为 BraceMatching。

2. 导入以下命名空间。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet1":::

3. 定义 `BraceMatchingTagger` 从类型继承的类 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet2":::

4. 添加文本视图的属性、源缓冲区、当前快照点和一组大括号对。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet3":::

5. 在标记构造函数中，设置属性并订阅视图更改事件 <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> 和 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> 。 在此示例中，出于演示目的，也在构造函数中定义了匹配对。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet4":::

6. 作为实现的一部分 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> ，请声明一个 TagsChanged 事件。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet5":::

7. 事件处理程序更新属性的当前脱字号位置 `CurrentChar` ，并引发 TagsChanged 事件。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet6":::

8. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>当当前字符为左大括号时，或在上一个字符为右大括号（如 Visual Studio 中）时，实现方法来匹配大括号。 当找到匹配项时，此方法将实例化两个标记，一个用于左大括号，另一个用于右大括号。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet7":::

9. 以下私有方法查找任何嵌套级别的匹配大括号。 第一种方法查找匹配左字符的接近字符：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet8":::

10. 以下 helper 方法查找与 close 字符匹配的开放字符：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet9":::

## <a name="implement-a-brace-matching-tagger-provider"></a>实现与标记提供程序匹配的大括号
 除了实现标记外，还必须实现和导出标记提供程序。 在这种情况下，提供程序的内容类型为 "text"。 因此，大括号匹配将出现在所有类型的文本文件中，但更完整的实现仅向特定内容类型应用大括号匹配。

### <a name="to-implement-a-brace-matching-tagger-provider"></a>实现与标记提供程序匹配的大括号

1. 声明从继承的标记提供程序 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> ，将其命名为 BraceMatchingTaggerProvider，然后将其导出为 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "text" 和 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> 的 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet10":::

2. 实现 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> 方法以实例化 BraceMatchingTagger。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet11":::

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 BraceMatchingTest 解决方案并在实验实例中运行它。

#### <a name="to-build-and-test-bracematchingtest-solution"></a>生成和测试 BraceMatchingTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

3. 创建一个文本文件并键入一些文本，其中包含匹配的大括号。

    ```
    hello {
    goodbye}

    {}

    {hello}
    ```

4. 将插入符号放置在左大括号前时，应突出显示这两个大括号和匹配的右大括号。 将光标置于右大括号之后时，应突出显示这两个大括号和匹配的左大括号。

## <a name="see-also"></a>另请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
