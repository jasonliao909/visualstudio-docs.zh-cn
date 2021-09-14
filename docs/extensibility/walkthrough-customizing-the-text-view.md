---
title: 演练：自定义文本视图 |Microsoft Docs
description: 使用本演练，了解如何通过修改其编辑器格式映射中的多个属性来自定义文本视图。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - customizing the view
ms.assetid: 32d32ac8-22ff-4de7-af69-bd46ec4ad9bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: fd60c6e9c6253a214de7a08173462895cdf29fc1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601024"
---
# <a name="walkthrough-customize-the-text-view"></a>演练：自定义文本视图
可以通过在其编辑器格式映射中修改以下任何属性来自定义文本视图：

- 指示器边距

- 插入插入符号

- 覆盖插入符号

- 选定的文本

- 非活动选定文本 (也就是说，所选文本丢失焦点) 

- 可见空白

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不会从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-mef-project"></a>创建 MEF 项目

1. 创建 c # VSIX 项目。  (在 "**新建 Project** " 对话框中，依次选择 " **Visual c #/扩展性**"、" **VSIX Project**"。 ) `ViewPropertyTest` 将解决方案命名为。

2. 将编辑器分类器项模板添加到项目。 有关详细信息，请参阅[使用编辑器项模板创建扩展](../extensibility/creating-an-extension-with-an-editor-item-template.md)。

3. 删除现有的类文件。

## <a name="define-the-content-type"></a>定义内容类型

1. 添加一个类文件并将其命名为 `ViewPropertyModifier`。

2. 然后，添加以下 `using` 指令：

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs" id="Snippet1":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb" id="Snippet1":::

3. 声明一个从继承的名为 `TestViewCreationListener` 的类 <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener> 。 将此类导出为以下属性：

   - <xref:Microsoft.VisualStudio.Utilities.ContentTypeAttribute> 指定此侦听器应用于的内容的类型。

   - <xref:Microsoft.VisualStudio.Text.Editor.TextViewRoleAttribute> 指定此侦听器的角色。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb" id="Snippet2":::

4. 在此类中，导入 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMapService> 。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs" id="Snippet3":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb" id="Snippet3":::

## <a name="change-the-view-properties"></a>更改视图属性

1. 设置方法， <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextViewCreationListener.TextViewCreated%2A> 以便在打开视图时更改视图属性。 若要进行更改，请首先找到 <xref:System.Windows.ResourceDictionary> 与要查找的视图的各个方面相对应的。 然后，在资源字典中更改相应的属性，并设置属性。 对方法的调用进行批处理，方法 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.SetProperties%2A> 是在 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.BeginBatchUpdate%2A> 设置属性之前调用方法，然后设置 <xref:Microsoft.VisualStudio.Text.Classification.IEditorFormatMap.EndBatchUpdate%2A> 属性。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_VSSDK/vssdkviewpropertytest/cs/viewpropertymodifier.cs" id="Snippet4":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VSSDK/vssdkviewpropertytest/vb/viewpropertymodifier.vb" id="Snippet4":::

## <a name="build-and-test-the-code"></a>生成和测试代码

1. 生成解决方案。

     在调试器中运行此项目时，将启动 Visual Studio 的第二个实例。

2. 创建一个文本文件并键入一些文本。

    - 插入插入符号应为洋红色，覆盖符号应为青绿色。

    - 指示器边距 (在文本视图的左侧) 应为浅绿色。

3. 选择键入的文本。 所选文本的颜色应为浅粉色。

4. 选择文本时，请单击文本窗口外的任意位置。 所选文本的颜色应为暗粉色。

5. 打开可见的空白。  (在 " **编辑** " 菜单上，指向 " **高级** "，然后单击 " **查看空白**) 。 在文本中键入某些选项卡。 应显示表示选项卡的红色箭头。

## <a name="see-also"></a>另请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
