---
title: 文档Windows窗体控件Office限制
description: 了解对文档Windows窗体控件方法和属性Microsoft Office限制。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], ActiveX legacy
- ActiveX controls [Office development in Visual Studio]
- Windows Forms controls [Office development in Visual Studio], limitations
- controls [Office development in Visual Studio], Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], unsupported properties and methods
- Toolbox [Office development in Visual Studio], unsupported controls
- user controls [Office development in Visual Studio], grouping controls
- Windows Forms controls [Office development in Visual Studio], Toolbox
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 8eddcb8273b1ff3c619de85c6f871d617d3c9a92
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122082915"
---
# <a name="limitations-of-windows-forms-controls-on-office-documents"></a>文档Windows窗体控件Office限制

添加到 Microsoft Office Word 文档或 Microsoft Office Excel 工作表的 Windows Forms 控件与添加到 Windows 窗体的 Windows 窗体控件之间存在一些差异。 例如，向文档添加控件时，、 和 等属性的行为与 <xref:Microsoft.Office.Tools.Word.Controls.Button> <xref:System.Windows.Forms.Control.Dock> <xref:System.Windows.Forms.Control.Anchor> <xref:System.Windows.Forms.Control.TabIndex> 预期不同。

其中许多差异是由在文档上承载Windows窗体控件的方式引起的。 将Windows窗体控件添加到文档时， 将嵌入一个 ActiveX 控件，该控件随后在文档中Windows [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 窗体控件。 "Windows窗体"控件不会直接嵌入文档中。

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="limitations-of-methods-and-properties-of-windows-forms-controls"></a>窗体控件的方法和Windows限制

Windows 窗体控件有许多方法和属性在文档上与在 Windows 窗体上不一样，因此建议不要使用它们。 例如，设置 属性（如 和 ）仅影响控件与容器控件ActiveX的位置，而 <xref:System.Windows.Forms.Control.Dock> <xref:System.Windows.Forms.Control.Anchor> 不会影响文档。 下面是 Word 和 Windows 窗体控件不支持的方法和属性Excel：

- 控件的不受Excel属性：

  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>

- Word 控件的方法和属性不受支持：

  - <xref:System.Windows.Forms.Control.Hide%2A>
  - <xref:System.Windows.Forms.Control.Show%2A>
  - <xref:System.Windows.Forms.Control.Anchor>
  - <xref:System.Windows.Forms.Control.Dock>
  - <xref:System.Windows.Forms.Control.Location>
  - <xref:System.Windows.Forms.Control.TabIndex>
  - <xref:System.Windows.Forms.Control.TabStop>
  - <xref:System.Windows.Forms.Control.TopLevelControl>
  - <xref:System.Windows.Forms.Control.Visible>

也不能设置与 Word 文档上的文本Windows窗体控件的 <xref:System.Windows.Forms.Control.Left> <xref:System.Windows.Forms.Control.Top> 或 属性。 Windows在下列情况下，窗体控件与文本一起添加：

- 以编程方式将控件添加到 Word 文档，并使用指定位置范围的方法。

- 在设计时Windows Word 文档添加一个窗体控件。 可以通过在设计器中修改 控件来更改此控件。

## <a name="differences-in-windows-forms-controls-on-office-documents"></a>文档Windows窗体控件Office差异

Windows窗体控件对文档的行为通常Office窗体上的行为相同，Windows存在一些差异。 下表描述了在文档上Windows窗体控件Office差异。

|功能|差|
|-------------------|----------------|
|控件选项卡顺序|无法按 Tab 键浏览放置在Excel或 Word 文档上的控件。|
|控制分组|不能使用 控件 <xref:System.Windows.Forms.GroupBox> 在文档上包含其他Office控件。 将多个单选按钮直接添加到文档时，单选按钮不是互斥的。 可以编写代码，使单选按钮互斥;但是，首选方法是将单选按钮添加到用户控件，然后将用户控件添加到文档。 有关详细信息，请参阅 Word 控件示例或 Excel 控件示例（Office[开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)）。|
|控件类型|Windows在文档中使用的窗体控件包装在 由 提供的类中，该类为控件提供特定于 Excel 或 Word 文档 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的其他功能。 例如，如果在工作表上具有Button Excel，请确保在引用或强制转换对象时将类型指定为 而不是 <xref:Microsoft.Office.Tools.Excel.Controls.Button> <xref:System.Windows.Forms.Button> 。|
|控制位置和大小|控件的大小和位置由容器和控件的一ActiveX确定。 ActiveX控件属性的值不同于窗体控件的等效Windows属性。 设置控件的 、、 或 属性时，它以点（而不是像素） `Top` `Left` `Height` `Width` 度量。|
|控制 Word 文档上的位置|如果将控件添加到基于流的布局，请记住，当内容更改时，控件将随内容一起流动。 从工具箱拖动控件时，不能将控件定位到该段落，因为该控件与文本一起添加到 Word 文档中。 如果使用另一种方法添加控件（例如双击控件），则根据为插入图片设置的 Word 选项插入控件。<br /><br /> 不能设置 `Left` 与文本内 `Top` 联的控件的 或 属性。<br /><br /> 不能将控件放在页眉或页脚中，也不能放在子文档内。|
|控制事件|选择控件后，它将按以下顺序引发事件：<br /><br /> 1.  `Enter`<br />2.  `GotFocus`<br /><br /> 取消选择控件后，它将按以下顺序引发事件：<br /><br /> 1.  `Leave`<br />2.  `Validating`<br />3.  `Validated`<br />4.  `LostFocus`|
|控制缩放|将文档的缩放设置更改为除 100% 外的其他任何内容时，将禁用控件，尽管它们似乎随文档一起缩放。 例如，如果在文档处于 130% 缩放时单击按钮，则会显示一条消息，指出控件已禁用，直到缩放设置为 100%。 将缩放更改为 100% 时，控件将正常工作。|
|控件属性值|尽管窗体上的控件Windows设置为整数值，但是对于 Word 文档中的控件，它们设置为单个 。 在Excel中，控件的属性值设置为双精度值。 如果工作表上控件的 和 属性超过工作表或屏幕的大小， `Height` `Width` 则值将被截断。|
|控制大小调整|如果使用八个大小调整句柄中的一个调整文档上的控件大小，在重新选择控件之前，新控件维度不会反映在"属性"窗口中。|
|控制行为|拆分工作表Excel工作表上的控件的行为可能无法预测。 例如，只能在其中一个窗口中访问工作表 <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> 上的 。|
|控件命名|不能使用保留字命名控件。 例如，如果将 添加到工作表，并且将名称更改为 <xref:Microsoft.Office.Tools.Excel.Controls.Button> **"系统"，** 则生成项目时出错。|
|以编程方式添加控件|请勿使用 控件的构造函数运行时向文档添加控件。 请改为使用 所提供的帮助程序方法 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 例如，使用 <xref:Microsoft.Office.Tools.Excel.ControlExtensions.AddButton%2A> 方法将按钮添加到工作表。 如果要添加这些帮助程序方法不支持的控件，可以使用 `AddControl` 方法。 有关详细信息，请参阅[向Office添加控件。](../vsto/adding-controls-to-office-documents-at-run-time.md)|
|复制控件|如果复制Windows窗体控件并运行时将其粘贴到文档中，则ActiveX控件的空容器将粘贴到文档中。 "Windows窗体"控件不会出现在新位置，并且原始控件后面的代码不会复制到该控件ActiveX容器。|

## <a name="limitations-in-document-level-projects"></a>文档级项目中的限制

对文档使用 Windows窗体控件的一些限制对于文档级项目是唯一的。

### <a name="control-support-at-design-time"></a>设计时的控制支持

当Windows设计器中打开 Excel 工作表或Word 文档时，某些窗体窗体控件将从工具箱Visual Studio中移除。 这是因为存在技术限制，或者该功能已在 Word 或 Excel。 Excel和 Word 项目支持所有 Windows 窗体控件以及当文档具有焦点时显示在工具箱中的其他组件，并且还可以将第三方控件添加到工作表或文档。

> [!NOTE]
> 当文档受保护时， **将从** 工具箱中删除所有控件。 有关文档保护的信息，请参阅 [文档级解决方案 中的文档保护](../vsto/document-protection-in-document-level-solutions.md)。

> [!NOTE]
> 第三方控件必须将 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 属性设置为 **true，** 才能在 Office 解决方案。

以下控件和组件在工具箱中 **不可用**：

- <xref:System.Windows.Forms.BindingNavigator>

- <xref:System.Windows.Forms.ContextMenuStrip>

- <xref:System.Windows.Forms.DataGrid>

- <xref:System.DirectoryServices.DirectoryEntry>

- <xref:System.DirectoryServices.DirectorySearcher>

- <xref:System.Windows.Forms.ErrorProvider>

- <xref:System.Diagnostics.EventLog>

- <xref:System.IO.FileSystemWatcher>

- <xref:System.Windows.Forms.FlowLayoutPanel>

- <xref:System.Windows.Forms.GroupBox>

- <xref:System.Windows.Forms.MainMenu>

- <xref:System.Windows.Forms.MenuStrip>

- <xref:System.Messaging.MessageQueue>

- <xref:System.Windows.Forms.NotifyIcon>

- <xref:System.Windows.Forms.PageSetupDialog>

- <xref:System.Windows.Forms.Panel>

- <xref:System.Diagnostics.PerformanceCounter>

- <xref:System.Windows.Forms.PrintDialog>

- <xref:System.Drawing.Printing.PrintDocument>

- <xref:System.Windows.Forms.PrintPreviewControl>

- <xref:System.Diagnostics.Process>

- <xref:System.Windows.Forms.RichTextBox>

- <xref:System.IO.Ports.SerialPort>

- <xref:System.ServiceProcess.ServiceController>

- <xref:System.Windows.Forms.SplitContainer>

- <xref:System.Windows.Forms.Splitter>

- <xref:System.Windows.Forms.StatusBar>

- <xref:System.Windows.Forms.StatusStrip>

- <xref:System.Windows.Forms.TabControl>

- <xref:System.Windows.Forms.TableLayoutPanel>

- <xref:System.Timers.Timer>

- <xref:System.Windows.Forms.Timer>

- <xref:System.Windows.Forms.ToolBar>

- <xref:System.Windows.Forms.ToolStrip>

- <xref:System.Windows.Forms.ToolStripContainer>

- <xref:System.Windows.Forms.ToolStripDropDown>

- <xref:System.Windows.Forms.ToolStripDropDownMenu>

- <xref:System.Windows.Forms.ToolStripPanel>

### <a name="support-for-legacy-activex-controls"></a>支持旧版ActiveX控件

如果创建使用现有 Word Office或包含 ActiveX 控件的 Excel 工作簿的文档级项目，则ActiveX控件的功能不会丢失;但是，不支持从ActiveX将新的控件添加到Visual Studio。 例如，如果 Word 文档具有运行 Visual Basic for Applications ( VBA) 宏的"控制"工具箱中的按钮，则文档在 Office 项目中使用后，它将继续运行宏。 但是，建议删除 ActiveX 和 VBA 宏，并将其替换为Windows窗体控件和托管代码。

## <a name="see-also"></a>请参阅

- [文档上的Office控件](../vsto/controls-on-office-documents.md)
- [Windows文档上的窗体Office概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [运行时向Office文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：添加Windows窗体控件以Office文档](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
