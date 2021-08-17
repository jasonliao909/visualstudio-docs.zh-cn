---
title: 演练：显示匹配的大括号|Microsoft Docs
description: 了解如何使用本演练在语言的上下文中定义大括号，以及如何将大括号匹配标记应用于文本内容类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - brace matching
ms.assetid: 5af08ac7-1d08-4ccf-997e-01aa6cb3d3d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: dacf3ffff56580e445f2eeda851d30082ba90f45
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049137"
---
# <a name="walkthrough-display-matching-braces"></a>演练：显示匹配的大括号
实现基于语言的功能，例如，通过定义要匹配的大括号来实现大括号匹配，以及当符号位于其中一个大括号上时，向匹配大括号添加文本标记标记。 可以在语言的上下文中定义大括号、定义自己的文件扩展名和内容类型，并仅将标记应用于该类型，或将标记应用于现有内容类型 (如"text") 。 下面的演练演示如何将大括号匹配标记应用于"text"内容类型。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-managed-extensibility-framework-mef-project"></a>创建一Managed Extensibility Framework (MEF) 项目

#### <a name="to-create-a-mef-project"></a>创建 MEF 项目

1. 创建编辑器分类器项目。 将解决方案命名为 `BraceMatchingTest`。

2. 向项目添加编辑器分类器项模板。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="implement-a-brace-matching-tagger"></a>实现大括号匹配标记器
 若要获取类似于在 Visual Studio 中使用的大括号突出显示效果，可以实现 类型的标记 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 器。 下面的代码演示如何在任何嵌套级别定义大括号对的标记器。 本示例在标记器构造函数中定义了 [] 和 的大括号对，但在完整语言实现中，将在语言规范中定义相关大括号 {} 对。

### <a name="to-implement-a-brace-matching-tagger"></a>实现大括号匹配标记器

1. 添加一个类文件，将其命名为 BraceMatching。

2. 导入以下命名空间。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet1":::

3. 定义从 `BraceMatchingTagger` 类型继承的 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 类 <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet2":::

4. 为文本视图、源缓冲区、当前快照点以及一组大括号对添加属性。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet3":::

5. 在标记器构造函数中，设置属性并订阅视图更改事件 <xref:Microsoft.VisualStudio.Text.Editor.ITextCaret.PositionChanged> 和 <xref:Microsoft.VisualStudio.Text.Editor.ITextView.LayoutChanged> 。 此示例中，出于说明目的，匹配对也在 构造函数中定义。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet4":::

6. 作为实现一 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 部分，声明 TagsChanged 事件。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet5":::

7. 事件处理程序将更新 属性的当前点点 `CurrentChar` 位置，并引发 TagsChanged 事件。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet6":::

8. 实现 方法，在当前字符为左大括号或上一个字符为右大括号时匹配大括号，如 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A> Visual Studio。 找到匹配项后，此方法将实例化两个标记，一个标记用于左大括号，另一个标记用于右大括号。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet7":::

9. 以下私有方法在任何嵌套级别查找匹配的大括号。 第一种方法查找与打开的字符匹配的关闭字符：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet8":::

10. 以下帮助程序方法查找与关闭字符匹配的打开字符：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet9":::

## <a name="implement-a-brace-matching-tagger-provider"></a>实现大括号匹配标记器提供程序
 除了实现标记器外，还必须实现和导出标记器提供程序。 在这种情况下，提供程序的内容类型为"text"。 因此，大括号匹配将显示在所有类型的文本文件中，但更完整的实现仅将大括号匹配应用于特定的内容类型。

### <a name="to-implement-a-brace-matching-tagger-provider"></a>实现大括号匹配标记器提供程序

1. 声明继承自 的标记器提供程序，将它命名 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider> BraceMatchingTaggerProvider，然后使用 "text" 和 的 导出 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> <xref:Microsoft.VisualStudio.Text.Tagging.TextMarkerTag> 它。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet10":::

2. 实现 <xref:Microsoft.VisualStudio.Text.Tagging.IViewTaggerProvider.CreateTagger%2A> 方法以实例化 BraceMatchingTagger。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkbracematchingtest/cs/bracematching.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkbracematchingtest/vb/bracematching.vb" id="Snippet11":::

## <a name="build-and-test-the-code"></a>生成并测试代码
 若要测试此代码，请生成 BraceMatchingTest 解决方案，并运行它在实验实例中。

#### <a name="to-build-and-test-bracematchingtest-solution"></a>生成和测试 BraceMatchingTest 解决方案

1. 生成解决方案。

2. 在调试器中运行此项目时，将启动第二Visual Studio实例。

3. 创建文本文件并键入一些包含匹配大括号的文本。

    ```
    hello {
    goodbye}

    {}

    {hello}
    ```

4. 将点线定位到左大括号之前时，应突出显示该大括号和匹配的右大括号。 将光标置于右大括号之后时，应突出显示该大括号和匹配的左大括号。

## <a name="see-also"></a>请参阅
- [演练：将内容类型链接到文件扩展名](../extensibility/walkthrough-linking-a-content-type-to-a-file-name-extension.md)
