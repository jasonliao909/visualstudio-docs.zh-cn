---
title: 如何：将架构映射到 Visual Studio 中的工作表
description: 了解在 Visual Studio 打开工作表时，如何将 XML 架构映射到 Microsoft Office Excel 工作表。
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
# <a name="how-to-map-schemas-to-worksheets-inside-visual-studio"></a>如何：将架构映射到 Visual Studio 中的工作表
  在 Visual Studio 中打开工作表时，可以将 XML 架构映射到工作表。 使用与在 Visual Studio 之外打开工作簿时使用的相同 Microsoft Office Excel 工具。 无论在创建 Excel 解决方案之前还是之后将架构映射到工作表，Office 项目都将创建相同的对象。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> 在 Excel 解决方案中，不能使用多部分 XML 架构。

## <a name="to-map-an-xml-schema-to-an-excel-worksheet-in-visual-studio"></a>将 XML 架构映射到 Visual Studio 中的 Excel 工作表

1. 在 Visual Studio 内打开 Excel 工作簿或模板项目。

2. 在工作表中单击，将焦点移到设计器中。

3. 在功能区上，单击 **“开发人员”** 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [如何：在功能区上显示 "开发人员" 选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

4. 在 " **XML** " 组中，单击 " **源**"。

     此时将打开 " **XML 源** " 窗口。

5. 在 " **Xml 源**" 窗口中，单击 " **xml 地图**。

     此时将打开 " **XML 地图**" 对话框。

6. 在 " **XML 地图**" 对话框中，单击 "**添加**"。

7. 浏览到您的架构文件，选择它，然后单击 " **打开**"。

8. 单击“确定”。

     架构在 " **XML 源** " 窗口中表示。 在您的项目中，将 <xref:System.Data.DataSet> 基于架构生成类型化，并 <xref:System.Windows.Forms.BindingSource> 创建一个。

9. 将元素从 " **XML 源** " 窗口拖到您要在其中创建相应控件的工作表中的位置。

     如果拖动非重复架构元素，Office 项目将生成 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 自动绑定到的控件 <xref:System.Windows.Forms.BindingSource> 。

     如果拖动重复架构元素，Office 项目将生成一个 <xref:Microsoft.Office.Tools.Excel.ListObject> 不会自动绑定到数据源的控件。 有关详细信息，请参阅 [文档级自定义项中的 XML 架构和数据](../vsto/xml-schemas-and-data-in-document-level-customizations.md)。

## <a name="see-also"></a>请参阅
- [如何：将架构映射到 Visual Studio 中的 Word 文档](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [文档级自定义项中的 XML 架构和数据](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
