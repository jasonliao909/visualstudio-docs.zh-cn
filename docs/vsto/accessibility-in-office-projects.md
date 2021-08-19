---
title: Office 项目中的辅助功能
description: 了解 Microsoft Office 项目如何包含许多辅助功能，这些功能使你能够构建满足标准辅助功能要求的自定义解决方案。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, accessibility
- shortcut keys [Office development in Visual Studio]
- Ribbon [Office development in Visual Studio], shortcut keys
- accessibility [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 440eb9ee0e5d228280cc8a8052abc3e7267e681e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122059889"
---
# <a name="accessibility-in-office-projects"></a>Office 项目中的辅助功能

Microsoft Visual Studio 和 Microsoft Office 包括许多辅助功能，使你能够构建满足标准辅助功能要求的自定义解决方案。 Microsoft 公布了 Web 上的辅助功能指导原则。 有关详细信息，请参阅 [辅助功能网站](https://www.microsoft.com/accessibility/)。

在大多数情况下，Visual Studio 中的 Office 项目可满足辅助功能标准或公开可设置为使解决方案可访问的属性。 但有些功能的可访问性有限。

[!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="accessibility-at-design-time"></a>设计时的可访问性

### <a name="use-shortcut-keys-in-document-level-projects"></a>使用文档级项目中的快捷键
 在 Visual Studio 中打开 Microsoft Office Word 文档或 Microsoft Office Excel 工作簿时，一次只能有一个应用程序收到快捷键命令。 默认情况下，Visual Studio 会接收所有快捷键命令，但可以通过在 "**选项**" 对话框的 "**键盘设置**" 页上选择 "**动态键盘方案**"，使 Word 或 Excel 在文档具有焦点时接收它们 有关详细信息，请参阅[Microsoft Office Word 键盘、Microsoft Office 键盘设置、"选项" 对话框](../vsto/microsoft-office-word-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)和[Microsoft Office Excel 键盘、Microsoft Office 键盘设置、"选项" 对话框](../vsto/microsoft-office-excel-keyboard-microsoft-office-keyboard-settings-options-dialog-box.md)。

### <a name="display-shortcut-keys-for-the-ribbon-in-document-level-projects"></a>在文档级项目中显示功能区的快捷键
 当在 Visual Studio 中打开 Word 文档或 Excel 工作簿时，您不能按 **Alt** 键来查看功能区上的选项卡和控件的快捷键。 若要在设计器中打开文档或工作簿时查看快捷键，请执行以下步骤。

#### <a name="to-view-shortcut-keys-for-ribbon-tabs-and-controls-in-the-designer"></a>在设计器中查看功能区选项卡和控件的快捷键

1. 在 Visual Studio 中，单击 "**工具**" 菜单上的 "**选项**"。

2. 展开 " **Office 工具**" 节点，并根据需要选择 **Microsoft Office Excel 键盘** 或 **Microsoft Office Word 键盘**。

3. 选择 " **动态键盘方案**"。

     此时将显示一条消息，表明必须重新启动 Visual Studio 才能使更改生效。

4. 单击“确定”。

5. 重新启动 Visual Studio，然后重新打开项目。

6. 打开项目的文档或工作簿设计器。

7. 按 **F6** 显示功能区的快捷键。

## <a name="accessibility-at-run-time"></a>运行时辅助功能

### <a name="windows-forms-controls-on-office-documents"></a>WindowsOffice 文档上的窗体控件
 Windows窗体控件公开可访问性属性，以便将控件的相关信息提供给辅助功能，如屏幕阅读器。 当控件位于文档级自定义项中的 Office 文档上时，可以利用这些可访问性属性。 有关详细信息，请参阅为[Windows 窗体上的控件提供辅助功能信息](/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form)。

 但是，当 Windows 窗体控件承载在 Excel 工作簿或 Word 文档上时，在运行时有一些可访问性限制：

- 不能从一个控件向另一个控件进行 tab。

- 将文档的缩放设置更改为100% 之外的任何内容时，将禁用文档上的控件。

  有关文档上 Windows 窗体控件的限制的信息，请参阅[Office 文档上 Windows 窗体控件的限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)。

### <a name="actions-panes-and-custom-task-panes"></a>操作窗格和自定义任务窗格
 当操作窗格或自定义任务窗格有焦点时，访问控件的方式与访问 Windows 窗体应用程序上的控件的方式相同。 若要在操作窗格和文档之间移动光标，可以按 **F6**。

 有关操作窗格和自定义任务窗格的详细信息，请参阅 [操作窗格概述](../vsto/actions-pane-overview.md) 和 [自定义任务窗格](../vsto/custom-task-panes.md)。

### <a name="display-modes"></a>显示模式

Visual Studio 具有与显示模式相关的以下限制：

- 将文档的缩放设置更改为100% 之外的任何内容时，将禁用 Word 文档或 Excel 工作表上的控件。

- 如果用户将计算机的辅助功能选项更改为 **使用高对比度**，则 "**新建 Project** " 对话框不会正确显示控件。

可以使用放大镜来克服这些限制。 放大镜是 Windows 中的显示实用程序，用于创建一个显示放大的屏幕部分的单独窗口。

## <a name="see-also"></a>请参阅

- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [为残障人士提供的辅助功能](../ide/reference/accessibility-features-of-visual-studio.md)
- [Visual Studio 的辅助功能](../ide/reference/accessibility-features-of-visual-studio.md)