---
title: 使用 VSTO 外接程序向文档添加自定义 XML 部件
description: 了解如何通过在 VSTO 外接程序中创建自定义 xml 部件，来将 XML 数据存储在以下类型的文档中。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], custom XML parts
- Office documents [Office development in Visual Studio, custom XML parts
- Word [Office development in Visual Studio], custom XML parts
- PowerPoint [Office development in Visual Studio], custom XML parts
- Excel [Office development in Visual Studio], custom XML parts
- custom XML parts [Office development in Visual Studio], adding
- documents [Office development in Visual Studio], custom XML parts
- application-level add-ins [Office development in Visual Studio], custom XML parts
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 9df71329ecf3058b3dd9cf9d9dfa86e6eae43888ae4c5b782c9e229753e6a594
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121268269"
---
# <a name="how-to-add-custom-xml-parts-to-documents-by-using-vsto-add-ins"></a>如何：使用 VSTO 外接程序向文档添加自定义 XML 部件
  通过在 VSTO 外接程序中创建自定义 XML 部件，可以将 XML 数据存储在以下类型的文档中：

- Microsoft Office Excel 工作簿。

- Microsoft Office Word 文档。

- Microsoft Office PowerPoint 演示文稿。

  有关详细信息，请参阅 [自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)。

  **适用于：** 本主题中的信息适用于 Excel、PowerPoint 和 Word 的应用程序级项目。 有关详细信息，请参阅[通过 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。

## <a name="to-add-a-custom-xml-part-to-an-excel-workbook"></a>向 Excel 工作簿添加自定义 XML 部件

1. 向工作簿中的 <xref:Microsoft.Office.Core.CustomXMLPart> 集合添加新 <xref:Microsoft.Office.Interop.Excel._Workbook.CustomXMLParts%2A> 对象。 <xref:Microsoft.Office.Core.CustomXMLPart> 包含你希望存储在工作簿中的 XML 字符串。

     下面的代码示例向指定工作簿添加自定义 XML 部件。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_addcustomxmlpartexcelapplevel/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartExcelAppLevel/ThisAddIn.cs" id="Snippet1":::

2. 将 `AddCustomXmlPartToWorkbook` 方法添加到 `ThisAddIn` Excel VSTO 外接程序项目中的类。

3. 从项目中的其他代码调用该方法。 例如，若要在用户打开工作簿时创建自定义 XML 部件，可从 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> 事件的事件处理程序调用该方法。

## <a name="to-add-a-custom-xml-part-to-a-word-document"></a>向 Word 文档添加自定义 XML 部件

1. 向文档中的 <xref:Microsoft.Office.Core.CustomXMLPart> 集合添加新的 <xref:Microsoft.Office.Interop.Word._Document.CustomXMLParts%2A> 对象。 <xref:Microsoft.Office.Core.CustomXMLPart> 包含你希望存储在文档中的 XML 字符串。

     下面的代码示例向指定文档添加自定义 XML 部件。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartWordAppLevel/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartWordAppLevel/ThisAddIn.cs" id="Snippet1":::

2. 将 `AddCustomXmlPartToDocument` 方法添加到 `ThisAddIn` Word VSTO 外接程序项目中的类。

3. 从项目中的其他代码调用该方法。 例如，若要在用户打开文档时创建自定义 XML 部件，可从 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> 事件的事件处理程序调用该方法。

## <a name="to-add-a-custom-xml-part-to-a-powerpoint-presentation"></a>向 PowerPoint 演示文稿添加自定义 XML 部件

1. 将新的 <xref:Microsoft.Office.Core.CustomXMLPart> 对象添加到[Office。交互.PowerPoint ._Presentation](/previous-versions/office/developer/office-2010/ff760806%28v%3doffice.14%29)演示中的 CustomXMLParts 集合。 <xref:Microsoft.Office.Core.CustomXMLPart> 包含你希望存储在演示文稿中的 XML 字符串。

     下面的代码示例向指定演示文稿添加自定义 XML 部件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_AddCustomXmlPartPowerPointAppLevel/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_AddCustomXmlPartPowerPointAppLevel/ThisAddIn.vb" id="Snippet1":::

2. 将 `AddCustomXmlPartToPresentation` 方法添加到 `ThisAddIn` PowerPoint VSTO 外接程序项目中的类。

3. 从项目中的其他代码调用该方法。 例如，若要在用户打开演示文稿时创建自定义 XML 部件，请从 Office 的事件处理程序调用方法[。交互.PowerPoint。EApplication_Event AfterPresentationOpen](/previous-versions/office/developer/office-2010/ff762843(v=office.14))事件。

## <a name="robust-programming"></a>可靠编程
 为简单起见，此示例使用在方法中定义为局部变量的 XML 字符串。 通常，应从外部源（如文件或数据库）获取 XML。

## <a name="see-also"></a>请参阅
- [自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)
- [如何：向文档级自定义项添加自定义 XML 部件](../vsto/how-to-add-custom-xml-parts-to-document-level-customizations.md)
