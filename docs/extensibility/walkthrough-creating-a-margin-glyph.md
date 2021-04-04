---
title: 演练：创建边距标志符号 |Microsoft Docs
description: 使用本演练，了解如何使用自定义编辑器扩展自定义编辑器边距的外观。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - margin glyph
ms.assetid: 814185db-24f9-417f-b3b1-7c5aabb42b45
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ec5eecef40220c2cf2d4e3f1ece8eb5eb763bdeb
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106217406"
---
# <a name="walkthrough-create-a-margin-glyph"></a>演练：创建边距标志符号
您可以使用自定义编辑器扩展自定义编辑器边距的外观。 此演练在代码注释中出现 "todo" 一词时，将自定义标志符号放置在指示器边距上。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 c # VSIX 项目。  (在 " **新建项目** " 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX 项目**"。 ) 将解决方案命名为 `TodoGlyphTest` 。

2. 添加编辑器分类器项目项。 有关详细信息，请参阅 [使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="define-the-glyph"></a>定义标志符号
 通过运行接口定义标志符号 <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> 。

### <a name="to-define-the-glyph"></a>定义标志符号

1. 添加一个类文件并将其命名为 `TodoGlyphFactory`。

2. 使用声明添加以下代码。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet1":::

3. 添加一个名为 `TodoGlyphFactory` 的类，该类实现 <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactory> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet2":::

4. 添加定义标志符号尺寸的私有字段。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet3":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet3":::

5. `GenerateGlyph`通过定义 (UI) 元素的标志符号用户界面实现。 `TodoTag` 在本演练的后面部分定义。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet4":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet4":::

6. 添加一个名为 `TodoGlyphFactoryProvider` 的类，该类实现 <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider> 。 使用 <xref:Microsoft.VisualStudio.Utilities.NameAttribute> "TodoGlyph"、" <xref:Microsoft.VisualStudio.Utilities.OrderAttribute> VsTextMarker"、 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "code" 和 "TodoTag" 的 "导出此类 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet5":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet5":::

7. <xref:Microsoft.VisualStudio.Text.Editor.IGlyphFactoryProvider.GetGlyphFactory%2A>通过实例化实现方法 `TodoGlyphFactory` 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todoglyphfactory.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todoglyphfactory.vb" id="Snippet6":::

## <a name="define-a-todo-tag-and-tagger"></a>定义 Todo 标记和标记
 定义您在前面的步骤中定义的 UI 元素与指示器边距之间的关系。 创建标记类型，并使用标记器提供程序来将其导出。

### <a name="to-define-a-todo-tag-and-tagger"></a>定义 todo 标记和标记

1. 向项目中添加一个新的类文件并将其命名为 `TodoTagger` 。

2. 添加以下 import 语句。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet7":::

3. 添加名为的 `TodoTag` 的类。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet8":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet8":::

4. 修改名为 `TodoTagger` 的类，该类实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601> 类型 `TodoTag` 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet9":::

5. `TodoTagger`对于类，为 <xref:Microsoft.VisualStudio.Text.Classification.IClassifier> 要在分类范围中查找的文本添加和的私有字段。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet10":::

6. 添加设置分类器的构造函数。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet11":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet11":::

7. <xref:Microsoft.VisualStudio.Text.Tagging.ITagger%601.GetTags%2A>通过查找名称中包含 "comment" 一词并且文本包含搜索文本的所有分类范围来实现方法。 每当找到搜索文本时，将生成类型为的新 <xref:Microsoft.VisualStudio.Text.Tagging.TagSpan%601> `TodoTag` 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet12":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet12":::

8. 声明 `TagsChanged` 事件。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet13":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet13":::

9. 添加一个名为的类，该类 `TodoTaggerProvider` 实现 <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider> ，并将其导出为 <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> "Code" 和 <xref:Microsoft.VisualStudio.Text.Tagging.TagTypeAttribute> TodoTag 的。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet14":::

10. 导入 <xref:Microsoft.VisualStudio.Text.Classification.IClassifierAggregatorService> 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet15":::

11. <xref:Microsoft.VisualStudio.Text.Tagging.ITaggerProvider.CreateTagger%2A>通过实例化实现方法 `TodoTagger` 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdktodoglyphtest/cs/todotagger.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdktodoglyphtest/vb/todotagger.vb" id="Snippet16":::

## <a name="build-and-test-the-code"></a>生成和测试代码
 若要测试此代码，请生成 TodoGlyphTest 解决方案并在实验实例中运行它。

### <a name="to-build-and-test-the-todoglyphtest-solution"></a>生成和测试 TodoGlyphTest 解决方案

1. 生成解决方案。

2. 按 **F5** 运行项目。 将启动 Visual Studio 的第二个实例。

3. 确保显示指示器边距。  (单击 " **工具** " 菜单上的 " **选项**"。 在 " **文本编辑器** " 页上，确保已选择 " **指示器边距** "。 ) 

4. 打开包含注释的代码文件。 将 "todo" 一词添加到注释部分。

5. "代码" 窗口左侧的指示器边距中会显示浅蓝色的浅蓝色圆圈。
