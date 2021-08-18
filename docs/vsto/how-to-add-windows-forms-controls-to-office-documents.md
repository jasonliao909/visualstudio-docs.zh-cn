---
title: 如何：将Windows窗体控件添加到Office文档
description: 了解如何在设计时Windows窗体Microsoft Office Excel和Microsoft Office Word 文档。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Windows Forms controls [Office development in Visual Studio], adding
- controls [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], Windows Forms controls
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 11d5efde772a85681f21fc8b08586f014d96978d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122026273"
---
# <a name="how-to-add-windows-forms-controls-to-office-documents"></a>如何：向Windows添加窗体Office控件
  你可以在设计时在文档级项目中，将 Windows 窗体控件添加到 Microsoft Office Excel 和 Microsoft Office Word 文档。 运行时，可以在文档级自定义项和外接程序中添加VSTO控件。例如，可以将控件 <xref:Microsoft.Office.Tools.Excel.Controls.ComboBox> 添加到工作表，以便用户可以从选项列表中选择。

 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

 本主题介绍了以下任务：

- [在设计时添加控件](#designtime)

- [在文档级项目中运行时添加控件](#runtimedoclevel)

- [在外接程序中VSTO控件](#runtimeaddin)

## <a name="add-controls-at-design-time"></a><a name="designtime"></a> 在设计时添加控件
 有几种方式在设计时向文档级项目中的文档添加 Windows 窗体控件。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-drag-a-windows-forms-control-to-the-document"></a>若要将 Windows 窗体控件拖到文档

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅如何：在 Office[创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

2. 在"**工具箱"的**"公共控件"选项卡中，单击要添加的控件，并将其拖动到文档。

    > [!NOTE]
    > 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

### <a name="to-draw-a-windows-forms-control-on-the-document"></a>若要在文档中绘制 Windows 窗体控件

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅如何：在 Office[创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

2. 在" **工具箱"的** "公共控件 **"** 选项卡中，单击要添加的控件。

3. 在文档中，单击希望要定位的控件的左上角位置，然后拖动到要定位的控件的右下角位置。

     该控件将按指定的位置和大小添加到文档。

    > [!NOTE]
    > 在公式中选择控件Excel，在公式栏中 **("WinForms.Control.Host"，") "。**  此文本是必需的并且不应删除。

### <a name="to-add-a-windows-forms-control-to-the-document-by-single-clicking-the-control"></a>若要通过右键单击控件将 Windows 窗体控件添加到文档

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅如何：在 Office[创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

2. 在" **工具箱"的** "公共控件 **"** 选项卡中，单击要添加的控件

3. 在文档中，单击希望要添加的控件的位置。

     该控件将以默认大小添加到文档。

    > [!NOTE]
    > 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

### <a name="to-add-a-windows-forms-control-to-the-document-by-double-clicking-the-control"></a>若要通过双击控件将 Windows 窗体控件添加到文档

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅如何：在 Office[创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

2. 在"**工具箱"的**"公共控件"选项卡中，双击要添加的控件。

     该控件将被添加到位于文档或活动窗格中心位置处的文档。

    > [!NOTE]
    > 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

### <a name="to-add-a-windows-forms-control-to-the-document-by-pressing-the-enter-key"></a>通过按 enter Windows向文档添加窗体控件

1. 在 Visual Studio 中创建或打开 Excel 工作簿项目或 Word 文档项目，以使文档在设计器中可见。 有关创建项目的信息，请参阅如何：在 Office[创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

2. 在"**工具箱"的**"公共控件"选项卡中，单击要添加的控件，然后按 **Enter** 键。

     该控件将被添加到位于文档或活动窗格中心位置处的文档。

    > [!NOTE]
    > 当在 Excel 中选择一个控件时， **“公式栏”** 中将显示 **=EMBED("WinForms.Control.Host","")**。 此文本是必需的并且不应删除。

## <a name="add-controls-at-run-time-in-document-level-projects"></a><a name="runtimedoclevel"></a> 在文档级项目中运行时添加控件
 你可以在运行时以编程方式向文档添加 Windows 窗体控件。 在 Word 中，请使用 `ThisDocument` 类的 <xref:Microsoft.Office.Tools.Word.DocumentBase.Controls%2A> 属性的方法。 在Excel中，使用 <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Controls%2A> n 类的 属性 `Sheet` 的方法。 每种方法都具有好几个重载，使你能够以不同的方式指定控件的位置。

 当在运行时向文档添加 Windows 窗体控件时，关闭文档时该控件将不会保存在文档中。 你可以在下次打开文档时重新创建该控件。 有关详细信息，请参阅[向Office添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

### <a name="to-add-a-windows-forms-control-at-run-time"></a>在运行时添加 Windows 窗体控件

1. 使用名称为 Add (的方法，其中 control 类是要添加的 Windows Forms 控件的类名，例如 \<*control class*>  <xref:Microsoft.Office.Tools.Word.ControlExtensions.AddButton%2A>) 。

     下面的代码示例演示如何将 添加到文档级项目中 的 <xref:Microsoft.Office.Tools.Excel.Controls.Button> **单元格 C5** 中，以 `Sheet1` Excel。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet4":::

## <a name="add-controls-at-run-time-in-vsto-add-ins"></a><a name="runtimeaddin"></a>在外接程序中VSTO控件
 你可以在运行时以编程方式将 Windows 窗体控件添加到任何打开的文档。 首先，生成一个基于打开的文档或工作表的主机项。 然后，在 Word 中，使用新主机项的 <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> 属性的方法。 然后，在 Excel 中，使用新主机项的 <xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A> 属性的方法。 每种方法都具有好几个重载，使你能够以不同的方式指定控件的位置。

 当在运行时向文档添加 Windows 窗体控件时，关闭文档时该控件将不会保存在文档中。 你可以在下次打开文档时重新创建该控件。 有关详细信息，请参阅[向Office添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)。

 有关在外接程序项目中VSTO宿主项的信息，请参阅在 VSTO 外接程序中运行时扩展 Word 文档[和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

### <a name="to-add-a-windows-forms-control-at-run-time"></a>在运行时添加 Windows 窗体控件

1. 使用名称为 Add (的方法，其中 control 类是要添加的 Windows Forms 控件的类名，例如 \<*control class*>  <xref:Microsoft.Office.Tools.Word.ControlExtensions.AddButton%2A>) 。

    > [!NOTE]
    > 在VSTO或更高版本的外接程序项目中，必须先添加对Microsoft.Office.Tools.Excel.v4.0.Utilities.dll或Microsoft.Office.Tools.Word.v4.0.Utilities.dll[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 程序集的引用，然后才能访问Add \<*control class*> 方法。

     下面的代码示例演示了如何通过使用 Word VSTO 外接程序将 <xref:Microsoft.Office.Tools.Word.Controls.Button> 添加到活动文档的第一段。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet7":::

## <a name="see-also"></a>请参阅
- [Windows文档上的窗体Office概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [运行时向Office文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：调整工作表单元格中的控件大小](../vsto/how-to-resize-controls-within-worksheet-cells.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
