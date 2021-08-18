---
title: 文档级自定义项中的 XML 架构和数据
description: Microsoft Excel 和 Word 提供将架构映射到文档的功能，可以简化在文档中导入和导出 XML 数据的操作。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio]
- schemas [Office development in Visual Studio]
- XML [Office development in Visual Studio], XML schemas
- XML schemas [Office development in Visual Studio], about XML schemas and data
- Office development in Visual Studio, XML
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 3944655cd84f1034e2c3850514d45fdccf27a1ec
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122045952"
---
# <a name="xml-schemas-and-data-in-document-level-customizations"></a>文档级自定义项中的 XML 架构和数据
  **重要提示** 本主题中的关于 Microsoft Word 的信息是专门针对美国及其区域以外的个人和组织的权益和使用的，或者开发在上运行的程序 Microsoft Word （在2010年1月之前，microsoft 从 Microsoft Word 中的自定义 XML 删除了特定功能的实现。 对于在2010年1月10日之后使用、或开发 Microsoft Word 的程序 Microsoft Word 产品的美国或其所在区域中的个人或组织，可能无法读取或使用与有关的信息。对于该日期之前许可的产品，这些产品的行为并不相同，也不会在美国之外购买和许可。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Microsoft Office Excel 和 Microsoft Office 字提供将架构映射到文档的功能。 此功能可简化在文档中导入和导出 XML 数据的操作。

 Visual Studio 公开文档级自定义项中的映射架构元素作为编程模型中的控件。 对于 Excel，Visual Studio 添加了支持，以将控件绑定到数据库、Web 服务和对象中的数据。 对于 Word 和 Excel，Visual Studio 添加了对操作窗格的支持，可与架构映射文档一起使用，为解决方案创建更高级的最终用户体验。 有关详细信息，请参阅 [操作窗格概述](../vsto/actions-pane-overview.md)。

> [!NOTE]
> 在 Excel 解决方案中，不能使用多部分 XML 架构。

## <a name="objects-created-when-schemas-are-attached-to-excel-workbooks"></a>架构附加到 Excel 工作簿时创建的对象
 将架构附加到工作簿时，Visual Studio 会自动创建多个对象并将其添加到项目。 不应使用 Visual Studio 工具删除这些对象，因为这些对象由 Excel 管理。 若要删除它们，请从工作表中删除映射的元素或使用 Excel 工具分离架构。

 主要有两个对象：

- XML 架构 (XSD 文件) 。 对于工作簿中的每个架构，Visual Studio 向项目添加架构。 它在 **解决方案资源管理器** 中显示为具有 XSD 扩展的项目项。

- 类型化 <xref:System.Data.DataSet> 类。 此类是基于架构创建的。 此数据集类在 **类视图** 中可见。

## <a name="objects-created-when-schema-elements-are-mapped-to-excel-worksheets"></a>将架构元素映射到 Excel 工作表时创建的对象
 将架构元素从 " **XML 源**" 任务窗格映射到工作表时，Visual Studio 会自动创建多个对象并将其添加到项目中：

- 控件. 对于工作簿中的每个映射对象， <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 会在编程模型中创建一个控件，用于非重复架构元素) 或用于 <xref:Microsoft.Office.Tools.Excel.ListObject> 重复架构) 元素 (控件的控件 (。 <xref:Microsoft.Office.Tools.Excel.ListObject>只能通过从工作簿中删除映射和映射的对象来删除控件。 有关控件的详细信息，请参阅 [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

- BindingSource. <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>通过将非重复架构元素映射到工作表创建时，会创建一个， <xref:System.Windows.Forms.BindingSource> 并将 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 控件绑定到 <xref:System.Windows.Forms.BindingSource> 。 您必须将绑定 <xref:System.Windows.Forms.BindingSource> 到与映射到文档的架构匹配的数据源的实例，如创建的类型化类的实例 <xref:System.Data.DataSet> 。 通过设置 <xref:System.Windows.Forms.BindingSource.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> 在 " **属性** " 窗口中公开的和属性来创建绑定。

    > [!NOTE]
    > <xref:System.Windows.Forms.BindingSource>不会为对象创建 <xref:Microsoft.Office.Tools.Excel.ListObject> 。 您必须 <xref:Microsoft.Office.Tools.Excel.ListObject> 通过 <xref:System.Windows.Forms.BindingSource.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> 在 " **属性** " 窗口中设置和属性，手动将绑定到数据源。

### <a name="office-mapped-schemas-and-the-visual-studio-data-sources-window"></a>Office 映射的架构和 Visual Studio 数据源 "窗口
 Office 的映射架构功能和 "Visual Studio **数据源**" 窗口都可以帮助您在 Excel 工作表上显示数据，以进行报告或编辑。 在这两种情况下，都可以将数据元素拖动到 Excel 工作表。 这两种方法都创建了通过数据绑定 <xref:System.Windows.Forms.BindingSource> 到数据源（如 <xref:System.Data.DataSet> 或 web 服务）的控件。

> [!NOTE]
> 将重复架构元素映射到工作表时，Visual Studio 创建 <xref:Microsoft.Office.Tools.Excel.ListObject> 。 <xref:Microsoft.Office.Tools.Excel.ListObject>不会通过自动绑定到数据 <xref:System.Windows.Forms.BindingSource> 。 您必须 <xref:Microsoft.Office.Tools.Excel.ListObject> 通过 <xref:System.Windows.Forms.BindingSource.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> 在 " **属性** " 窗口中设置和属性，手动将绑定到数据源。

 下表显示了这两种方法之间的一些差异。

|XML 架构|“数据源”窗口|
|----------------|-------------------------|
|使用 Office 接口。|使用 Visual Studio 中的 "**数据源**" 窗口。|
|启用内置 Office 功能，用于从 XML 文件导入和导出数据。|必须以编程方式提供导入和导出功能。|
|您必须编写代码以用数据填充生成的控件。|从 " **数据源** " 窗口添加的控件具有自动生成的代码，用于填充这些控件以及使用数据库服务器时所需的连接字符串。|

## <a name="behavior-when-schemas-are-attached-to-word-documents"></a>将架构附加到 Word 文档时的行为
 将架构附加到文档级 Office 项目中使用的 Word 文档时，不会创建数据对象。 但是，当您将架构元素映射到文档时，将创建控件。 控件的类型取决于您映射的元素类型;重复元素生成 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件，而非重复元素生成 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件。 有关详细信息，请参阅 [XMLNodes control](../vsto/xmlnodes-control.md) 和 [XMLNode control](../vsto/xmlnode-control.md)。

## <a name="deployment-of-solutions-that-include-xml-schemas"></a>部署包含 XML 架构的解决方案
 你应创建一个安装程序来部署使用映射到文档的 XML 架构的解决方案。 安装程序应在用户计算机上的架构库中注册架构。 如果未注册该架构，则该解决方案仍将起作用，因为 Word 将根据用户打开文档时该文档中的元素生成临时架构。 但是，用户将无法执行验证或保存用于创建项目的架构。 有关安装程序的详细信息，请参阅 [部署应用程序、服务和组件](../deployment/deploying-applications-services-and-components.md)。

 你还可以将代码添加到你的项目，以检查架构是否在库中并已注册。 如果不是，则可以警告用户。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataWordVB/ThisDocument.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataWordCS/ThisDocument.cs" id="Snippet1":::

## <a name="see-also"></a>请参阅

- [如何：将架构映射到 Visual Studio 中的 Word 文档](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [如何：将架构映射到 Visual Studio 中的工作表](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
