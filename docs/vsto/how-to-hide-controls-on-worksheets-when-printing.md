---
title: 如何：打印时隐藏工作表上的控件
description: 了解在打印包含窗体控件的 Microsoft Office Excel工作表时，Windows控件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- controls [Office development in Visual Studio], hiding while printing
- printing [Office development in Visual Studio], hiding controls
- worksheets, hiding controls when printing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: f0095510b45da5029173db590611255f83ca4e6edcc3fb0be695754064a39c6e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394688"
---
# <a name="how-to-hide-controls-on-worksheets-when-printing"></a>如何：打印时隐藏工作表上的控件
  打印包含 Microsoft Office Excel 窗体控件Windows文档时，这些控件在打印的工作表上可见。 打印工作表时，可以隐藏控件。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> 如果隐藏显示数据的控件（如 ），则控件中的数据在打印 <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> 的工作表上不可见。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="to-hide-controls-when-a-worksheet-is-printed"></a>打印工作表时隐藏控件

1. 在设计器Excel或打开Visual Studio，并验证 **Sheet1** 在设计器中是否可见。 有关创建项目的信息，请参阅如何：在 Office[创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

2. 从" **工具箱"的** "公共控件 **"选项卡** 中， <xref:Microsoft.Office.Tools.Excel.Controls.Button> 将控件拖动到 上的单元格 `Sheet1` 。

3. 在" **属性"** 窗口中，将 <xref:Microsoft.Office.Tools.Excel.Controls.Button.PrintObject%2A> 属性设置为 **False**。

## <a name="see-also"></a>另请参阅
- [文档Office控件](../vsto/controls-on-office-documents.md)
- [Windows文档上的窗体Office概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [如何：添加Windows窗体控件以Office文档](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [如何：调整工作表单元格中的控件大小](../vsto/how-to-resize-controls-within-worksheet-cells.md)
