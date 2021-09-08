---
title: 教程 1：创建图片查看器
description: 了解如何生成从文件加载图片并将其显示在窗口中的应用。
ms.custom: SEO-VS-2020
ms.date: 10/16/2019
ms.assetid: 3071d6df-2b2f-4e95-ab68-bef727323136
ms.topic: tutorial
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: e19a66adaf2123879e07f784bfbc6b953956001d
ms.sourcegitcommit: 3d1143b007bf0ead80bf4cb3867bf89ab0ab5b53
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2021
ms.locfileid: "123397689"
---
# <a name="tutorial-1-create-a-picture-viewer"></a>教程 1：创建图片查看器

在本教程中，你将生成一个从文件加载图片并将其显示在窗口中的应用。 你将学习如何使用“Windows 窗体设计器”拖动控件（如窗体上的按钮和图片框）、设置控件属性，以及如何使用容器来轻松地调整窗体的大小。 您还将开始编写代码。

> [!NOTE]
> 本教程中同时涉及 C# 和 Visual Basic，因此请关注特定于你所用编程语言的信息。

本教程将指导你完成以下任务：

* 创建新项目。

* 测试（调试）应用程序。

* 向窗体中添加基本控件（如复选框和按钮）。

* 使用布局在窗体上放置控件。

* 向窗体中添加“打开文件”和“颜色”对话框。

* 使用 IntelliSense 和代码片段编写代码。

* 编写事件处理程序方法。

完成时，应用应如下图所示：

![你在本教程中创建的图片查看器应用](../ide/media/express_pictureviewerdone.png)

## <a name="tutorial-links"></a>教程链接

|Title|说明|
|-----------|-----------------|
|[步骤 1：创建 Windows 窗体应用项目](../ide/step-1-create-a-windows-forms-application-project.md)|首先创建 Windows 窗体应用项目。|
|[步骤 2：运行图片查看器应用](../ide/step-2-run-your-program.md)|运行你在上一步中创建的 Windows 窗体应用项目。|
|[步骤 3：设置窗体属性](../ide/step-3-set-your-form-properties.md)|使用“属性”窗口更改窗体的显示方式。|
|[步骤 4：使用 TableLayoutPanel 控件设置窗体布局](../ide/step-4-lay-out-your-form-with-a-tablelayoutpanel-control.md)|向窗体添加一个 `TableLayoutPanel` 控件。|
|[步骤 5：向窗体添加控件](../ide/step-5-add-controls-to-your-form.md)|向窗体添加控件，如 `PictureBox` 控件和 `CheckBox` 控件。 向窗体中添加按钮。|
|[步骤 6：命名按钮控件](../ide/step-6-name-your-button-controls.md)|将按钮重命名为更有意义的名称。|
|[步骤 7：向窗体添加对话框组件](../ide/step-7-add-dialog-components-to-your-form.md)|向窗体添加 `OpenFileDialog` 组件和 `ColorDialog` 组件。|
|[步骤 8：为“显示图片”按钮事件处理程序编写代码](../ide/step-8-write-code-for-the-show-a-picture-button-event-handler.md)|使用 IntelliSense 工具编写代码。|
|[步骤 9：检查代码、为代码添加注释和测试代码](../ide/step-9-review-comment-and-test-your-code.md)|评审并测试代码。 根据需要添加注释。|
|[步骤 10：为其他按钮和复选框编写代码](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md)|使用 IntelliSense 编写代码以使其他按钮和复选框工作。|
|[步骤 11：运行应用并尝试其他功能](../ide/step-11-run-your-program-and-try-other-features.md)|运行应用并设置背景色。 尝试其他功能，例如更改颜色、字体和边框。|

那里还有很好的免费视频学习资源供你使用。 要了解有关 C# 编程的详细信息，请参阅 [C# 基础知识：零基础开发](https://channel9.msdn.com/Series/C-Sharp-Fundamentals-Development-for-Absolute-Beginners)。 要了解有关 Visual Basic 编程的详细信息，请参阅 [Visual Basic 基础知识：零基础开发](https://channel9.msdn.com/Series/Visual-Basic-Development-for-Absolute-Beginners)。

## <a name="next-steps"></a>后续步骤

要开始学习本教程，请从 **[步骤 1：创建 Windows 窗体应用程序项目](../ide/step-1-create-a-windows-forms-application-project.md)** 开始。

## <a name="see-also"></a>请参阅

* [更多 C# 教程](../get-started/csharp/index.yml)
* [Visual Basic 教程](../get-started/visual-basic/index.yml)
* [C++ 教程](/cpp/get-started/tutorial-console-cpp)