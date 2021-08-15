---
title: 如何：将架构映射到 Visual Studio
description: 了解如何在工作表中的工作表打开Microsoft Office Excel XML 架构映射到Visual Studio。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Excel worksheets
- Excel [Office development in Visual Studio], XML schemas
- worksheets [Office development in Visual Studio], XML schemas
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 9fb7a8a2a3ae7a8b0f7f3898fdf5b13b105f58886f1d5586f98ad625cbaa5d0a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424119"
---
# <a name="how-to-map-schemas-to-worksheets-inside-visual-studio"></a>如何：将架构映射到 Visual Studio
  当工作表在工作表中打开时，可以将 XML 架构映射到Visual Studio。 使用在Microsoft Office Excel外部打开工作簿时使用的相同Visual Studio。 无论Office解决方案之前或之后将架构映射到工作表，项目都创建相同的Excel对象。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> 不能在解决方案中使用多部分 XML Excel架构。

## <a name="to-map-an-xml-schema-to-an-excel-worksheet-in-visual-studio"></a>将 XML 架构映射到 Excel 工作表Visual Studio

1. 打开Excel中的工作簿或模板Visual Studio。

2. 单击工作表，将焦点移动到设计器。

3. 在功能区上，单击 **“开发人员”** 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [功能区 上的"如何：显示开发人员"选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

4. 在 **XML 组中**，单击"源 **"。**

     "XML **源"** 窗口随即打开。

5. 在 **"XML 源"** 窗口中，单击 **"XML 地图"。**

     "XML **地图** 对话框随即打开。

6. 在 **"XML 地图"** 对话框中，单击"添加 **"。**

7. 浏览到架构文件，将其选中，然后单击"打开 **"。**

8. 单击“确定”。

     架构在 **"XML 源"窗口中** 表示。 在项目中，根据 <xref:System.Data.DataSet> 架构生成类型，并 <xref:System.Windows.Forms.BindingSource> 创建 。

9. 将元素从 **"XML 源** "窗口拖动到工作表中要创建相应控件的位置。

     如果拖动非重复架构元素，则Office生成自动绑定到 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 的控件 <xref:System.Windows.Forms.BindingSource> 。

     如果拖动重复的架构元素，则Office生成不自动绑定到数据源 <xref:Microsoft.Office.Tools.Excel.ListObject> 的控件。 有关详细信息，请参阅 [文档级自定义项](../vsto/xml-schemas-and-data-in-document-level-customizations.md)中的 XML 架构和数据。

## <a name="see-also"></a>另请参阅
- [如何：将架构映射到文档中的 Word Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [文档级自定义项中的 XML 架构和数据](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
