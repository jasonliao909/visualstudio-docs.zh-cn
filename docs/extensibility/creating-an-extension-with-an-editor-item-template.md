---
title: 使用编辑器项模板创建扩展|Microsoft Docs
description: 了解如何使用 Visual Studio SDK 中的项模板创建向编辑器添加分类器、修饰和边距的基本编辑器扩展。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: fa3b993b-ab95-47fa-a38b-b788f3a5b2d8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c75d0a86d92c88c850e3b8250e3ac3551a1b75b475db9032f282355711f74db2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121262992"
---
# <a name="create-an-extension-with-an-editor-item-template"></a>使用编辑器项模板创建扩展
可以使用包含在 Visual Studio SDK 中的项模板来创建向编辑器添加分类器、修饰和边距的基本编辑器扩展。 编辑器项模板适用于 Visual C# 或 VSIX Visual Basic项目。

## <a name="prerequisites"></a>先决条件
 从 2015 Visual Studio开始，不会从下载Visual Studio安装 Visual Studio SDK。 它作为可选功能包含在安装程序Visual Studio中。 也可稍后安装 VS SDK。 有关详细信息，请参阅安装[Visual Studio SDK。](../extensibility/installing-the-visual-studio-sdk.md)

## <a name="create-a-classifier-extension"></a>创建分类器扩展
 编辑器分类器项模板创建一个编辑器分类器，用于 (文本颜色，所有内容) 任何文本文件中。

1. 在"**新建Project** 对话框中，展开 **"Visual C#"** 或Visual Basic，**然后单击"****扩展性"。** 在"**模板"窗格中**，选择 **"VSIX Project"。** 在“名称”  框中键入 `TestClassifier`。 单击“确定”。

2. 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 转到"Visual C#**扩展性"节点**，然后选择"**编辑器分类器"。** 将默认文件名保留 (*EditorClassifier1.cs) 。*

3. 有四个代码文件，如下所示：

    - *EditorClassifier1.cs* 包含 `EditorClassifier1` 类。

    - *EditorClassifier1ClassificationDefinition.cs* 包含 `EditorClassifier1ClassificationDefinition` 类。

    - *EditorClassifier1Format.cs* 包含 `EditorClassifier1Format`  类。

    - *EditorClassifier1Provider.cs* 包含 `EditorClassifier1Provider` 类。

4. 生成项目并启动调试。 将显示该实例Visual Studio实例。

     如果打开文本文件，则所有文本都带有背景下划线。

## <a name="create-a-text-relative-adornment-extension"></a>创建文本相对修饰扩展
 编辑器文本修饰模板创建一个文本相对修饰，该装饰使用具有红色轮廓和蓝色背景的框修饰文本字符"a"的所有实例。 它是相对于文本的，因为框始终覆盖"a"字符，即使它们已移动或重新格式化。

1. 在"**新建Project** 对话框中，展开 **"Visual C#"** 或Visual Basic，**然后单击"****扩展性"。** 在"**模板"窗格中**，选择 **"VSIX Project"。** 在“名称”  框中键入 `TestAdornment`。 单击“确定”。

2. 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 转到"Visual C#**扩展性"节点**，然后选择"**编辑器文本修饰"。** 将默认文件名保留为 (*textAdornment1.cs/vb) 。*

3. 有两个代码文件，如下所示：

    - *TextAdornment1.cs* 包含 `TextAdornment1` 类。

    - *TextAdornment1TextViewCreationListener.cs* 包含 `TextAdornment1TextViewCreationListener` 类。

4. 生成项目并启动调试。 这将显示实验实例。 如果打开文本文件，则文本中所有"a"字符在蓝色背景上以红色大纲显示。

## <a name="create-a-viewport-relative-adornment-extension"></a>创建视区相对修饰扩展
 编辑器视区修饰模板创建一个视区相对装饰，该装饰将具有红色轮廓的装饰框添加到视区右上角。

> [!NOTE]
> **视区** 是当前显示的文本视图的区域。

### <a name="to-create-a-viewport-adornment-extension-by-using-the-editor-viewport-adornment-template"></a>使用编辑器视区修饰模板创建视区装饰扩展

1. 在"**新建Project** 对话框中，展开 **"Visual C#"** 或Visual Basic，**然后单击"****扩展性"。** 在"**模板"窗格中**，选择 **"VSIX Project"。** 在“名称”  框中键入 `ViewportAdornment`。 单击“确定”。

2. 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 转到"Visual C#**扩展性"节点**，然后选择"**编辑器视区修饰"。** 将默认文件名保留为 (*ViewportAdornment1.cs/vb*) 。

3. 有两个代码文件，如下所示：

    - *ViewportAdornment1.cs* 包含 `ViewportAdornment1` 类。

    - *ViewportAdornment1TextViewCreationListener.cs* 包含 `ViewportAdornment1TextViewCreationListener` 类

4. 生成项目并启动调试。 这将显示实验实例。 如果创建新的文本文件，视区右上角会显示一个边框为红色边框的绿色框。

## <a name="create-a-margin-extension"></a>创建边距扩展
 编辑器边距模板创建一个绿色边距，该边距与单词 **Hello world！ 一起显示。* 水平滚动条下方。

### <a name="to-create-a-margin-extension-by-using-the-editor-margin-template"></a>使用编辑器边距模板创建边距扩展

1. 在"**新建Project** 对话框中，展开 **"Visual C#"** 或Visual Basic，**然后单击"****扩展性"。** 在"**模板"窗格中**，选择 **"VSIX Project"。** 在“名称”  框中键入 `MarginExtension`。 单击“确定”。

2. 在“解决方案资源管理器”中，右键单击项目节点并选择“添加” > “新建项”  。 转到"Visual C#**扩展性"节点，** 然后选择"**编辑器边距"。** 将默认文件名保留 (EditorMargin1.cs/vb) 。

3. 有两个代码文件，如下所示：

    - *EditorMargin1.cs* 包含 `EditorMargin1` 类。

    - *EditorMargin1Factory.cs* 包含 `EditorMargin1Factory` 类。

4. 生成此项目并开始调试。 这将显示实验实例。 如果打开文本文件，水平滚动条下方会显示一个绿色边距，其单词为 **Hello EditorMargin1。**

## <a name="see-also"></a>另请参阅
- [语言服务和编辑器扩展点](../extensibility/language-service-and-editor-extension-points.md)
