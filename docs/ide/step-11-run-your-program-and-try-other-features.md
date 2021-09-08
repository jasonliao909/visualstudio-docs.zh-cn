---
title: 运行图片查看器应用并尝试其他功能
description: 在“创建图片查看器”教程中运行图片查看器应用并尝试其他功能。
ms.date: 09/11/2019
ms.custom: SEO-VS-2020
ms.assetid: 656614d0-4fe7-4a67-8edc-c10919377d09
ms.topic: tutorial
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 7b6784c96c8915c0d80149023a786e8c4bc20680
ms.sourcegitcommit: 3d1143b007bf0ead80bf4cb3867bf89ab0ab5b53
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2021
ms.locfileid: "123398394"
---
# <a name="step-11-run-your-picture-viewer-app-and-try-other-features"></a>步骤 11：运行图片查看器应用并尝试其他功能

图片查看器应用已完成并已做好运行准备。 可以运行应用并设置 <xref:System.Windows.Forms.PictureBox> 的背景色。 要了解更多信息，请尝试通过以下操作来改进应用程序：更改窗体的颜色、自定义按钮和复选框以及更改窗体的属性。

## <a name="how-to-run-your-app-and-set-the-background-color"></a>如何运行应用并设置背景色

1. 选择 F5，或者在菜单栏上依次选择“调试” > “启动调试”。

1. 在打开图片之前，请选择“设置背景色”按钮。 随即打开“颜色”对话框。

     ![“颜色”对话框](../ide/media/express_colordialog.png)<br/>“颜色”对话框
*

1. 选择一种要设置为 PictureBox 背景色的颜色。 仔细查看 `backgroundButton_Click()`（或 `BackgroundButton_Click()`）方法以了解其工作原理。

    > [!NOTE]
    > 通过将某个图片的 URL 粘贴到“打开文件”对话框中，可以从 Internet 加载该图片。 尝试找到一个带透明背景的图像，以便显示您的背景色。

1. 选择“清除图片”按钮以确保清除图片。 然后，选择“关闭”按钮退出应用。

## <a name="try-other-features"></a>尝试其他功能

* 使用“BackColor”属性更改窗体和按钮的颜色。

* 使用“Font”和“ForeColor”属性自定义按钮和复选框。

* 更改窗体的“FormBorderStyle”和“ControlBox”属性。

* 使用窗体的“AcceptButton”和“CancelButton”属性可使得在用户选择 Enter 或 Esc 键时自动选择这些按钮。 使应用在用户选择 Enter 时打开“打开文件”对话框，并在用户选择 Esc 时关闭此对话框。

## <a name="next-steps"></a>后续步骤

要更加深入地了解，请继续学习下面的教程：

> [!div class="nextstepaction"]
> [教程 2：创建计时数学测验](../ide/tutorial-2-create-a-timed-math-quiz.md)

要返回上一个教程步骤，请参阅[步骤 10：为其他按钮和复选框编写代码](../ide/step-10-write-code-for-additional-buttons-and-a-check-box.md)。

## <a name="see-also"></a>请参阅

* [更多 C# 教程](../get-started/csharp/index.yml)
* [更多 Visual Basic 教程](../get-started/visual-basic/index.yml)
* [C++ 教程](/cpp/get-started/tutorial-console-cpp)