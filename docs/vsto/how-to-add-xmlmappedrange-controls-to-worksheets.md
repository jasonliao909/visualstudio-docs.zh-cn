---
title: 如何：向工作表添加 XMLMappedRange 控件
description: 请注意，当您将 XML 元素映射到 Microsoft Office Excel 中的单元时，Visual Studio 会自动将 XmlMappedRange 控件添加到工作表中。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 8fa5b3037b29cf15537215c9bf623c57ac8a119d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106323"
---
# <a name="how-to-add-xmlmappedrange-controls-to-worksheets"></a>如何：向工作表添加 XMLMappedRange 控件
  将 XML 元素映射到 Microsoft Office Excel 中的单元时，Visual Studio 会自动将 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 控件添加到工作表中。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件在 "**工具箱**" 或 "**数据源**" 窗口中不可用。 此外，不能 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 以编程方式创建控件。

## <a name="to-add-an-xmlmappedrange-control-to-a-worksheet"></a>向工作表添加 XMLMappedRange 控件

1. 在 "Visual Studio 设计器" 中打开 Excel 工作簿。

2. 打开要在其中添加控件的工作表。

3. 在 " **开发人员** " 选项卡上，单击 " **源**"。

    > [!NOTE]
    > 如果功能区上不显示 " **开发人员** " 选项卡，则必须启用它。 有关详细信息，请参阅 [如何：在功能区上显示 "开发人员" 选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

     此时将显示 " **XML 源** " 任务窗格。

4. 在 " **Xml 源**" 任务窗格中，单击 " **xml 地图**。

5. 在 " **XML 地图**" 对话框中，单击 "**添加**"。

     此时将显示 " **XML 源** " 对话框。

6. 从 " **Xml 源** " 对话框中选择一个 xml 架构，并单击 " **打开**"。

     架构将添加到 " **XML 地图**" 对话框中。

7. 在 " **XML 地图**" 对话框中，单击 **"确定"**。

8. 将 " **XML 源** " 任务窗格中的元素拖到工作表上的单元格中。

     <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>创建并将其添加到项目。

    > [!NOTE]
    > 如果从 " **XML 源** " 任务窗格中拖动父元素， <xref:Microsoft.Office.Tools.Excel.ListObject> 则会创建一个控件。

## <a name="see-also"></a>请参阅
- [XmlMappedRange 控件](../vsto/xmlmappedrange-control.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [如何：将架构映射到 Visual Studio 中的工作表](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
