---
title: 文档级自定义项中的 XML 架构和数据
description: Microsoft Excel和 Word 提供将架构映射到文档的功能，并可以简化在文档中导入和导出 XML 数据。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664922"
---
# <a name="xml-schemas-and-data-in-document-level-customizations"></a>文档级自定义项中的 XML 架构和数据
  **重要** 本主题中针对 Microsoft Word 设置的信息专门供位于 美国 及其区域之外的个人和组织使用，或者使用或开发在 2010 年 1 月之前由 Microsoft 许可的 Microsoft Word 产品（当 Microsoft 从 Microsoft Word 中删除与自定义 XML 相关的特定功能的实现时）运行的程序。 有关 Microsoft Word 的信息不能由 美国 或其区域使用或开发在 2010 年 1 月 10 日之后由 Microsoft 许可的 Microsoft Word 产品运行的程序的个人或组织读取或使用;这些产品的行为与该日期之前许可的产品或购买和许可在应用程序外部使用的产品美国。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 Microsoft Office Excel和 Microsoft Office Word 提供将架构映射到文档的功能。 此功能可以简化在文档中导入和导出 XML 数据。

 Visual Studio将文档级自定义项中的映射架构元素公开为编程模型中的控件。 对于Excel，Visual Studio添加了对将控件绑定到数据库、Web 服务和对象中数据的支持。 对于 Word 和 Excel，Visual Studio添加了对操作窗格的支持，这些窗格可用于架构映射文档，为解决方案创建增强的最终用户体验。 有关详细信息，请参阅操作 [窗格概述](../vsto/actions-pane-overview.md)。

> [!NOTE]
> 不能在解决方案中使用多部分 XML Excel架构。

## <a name="objects-created-when-schemas-are-attached-to-excel-workbooks"></a>将架构附加到工作簿时Excel对象
 将架构附加到工作簿时，Visual Studio自动创建多个对象并添加到项目中。 不应使用这些工具删除这些Visual Studio，因为它们由 Excel。 若要删除这些元素，请从工作表中删除映射的元素，或者使用Excel架构。

 有两个主要对象：

- XML 架构 (XSD 文件) 。 对于工作簿中的每个架构，Visual Studio向项目添加架构。 这显示为项目项，其 XSD **扩展名** 解决方案资源管理器。

- 类型化 <xref:System.Data.DataSet> 类。 此类是基于架构创建的。 此数据集类在 中 **类视图。**

## <a name="objects-created-when-schema-elements-are-mapped-to-excel-worksheets"></a>将架构元素映射到工作表时Excel对象
 将架构元素从 **"XML** 源"任务窗格映射到工作表时，Visual Studio自动创建多个对象并添加到项目中：

- 控制。 对于工作簿中每个映射的对象， (为非重复架构元素) 或用于重复架构元素的 (控件) 在编程模型中 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> <xref:Microsoft.Office.Tools.Excel.ListObject> 创建。 <xref:Microsoft.Office.Tools.Excel.ListObject>只有从工作簿中删除映射和映射对象，才能删除该控件。 有关控件详细信息，请参阅主机 [项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

- BindingSource。 通过将非重复架构元素映射到工作表来创建 时，将创建 ，并且控件 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> <xref:System.Windows.Forms.BindingSource> 绑定到 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> <xref:System.Windows.Forms.BindingSource> 。 必须将 绑定到数据源的实例，该实例与映射到文档的架构匹配，例如所创建的 <xref:System.Windows.Forms.BindingSource> 类型类 <xref:System.Data.DataSet> 的实例。 通过设置 和 属性来创建绑定 <xref:System.Windows.Forms.BindingSource.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> ，这些属性在"属性"窗口中公开。

    > [!NOTE]
    > <xref:System.Windows.Forms.BindingSource>不为 对象 <xref:Microsoft.Office.Tools.Excel.ListObject> 创建 。 必须通过在"属性"窗口中设置 和 属性，手动 <xref:Microsoft.Office.Tools.Excel.ListObject> <xref:System.Windows.Forms.BindingSource.DataSource%2A> 将 <xref:System.Windows.Forms.BindingSource.DataMember%2A> 绑定到数据源。

### <a name="office-mapped-schemas-and-the-visual-studio-data-sources-window"></a>Office映射的架构和"Visual Studio数据源"窗口
 数据源的映射架构Office和"Visual Studio **数据源**"窗口都可以帮助你在报表或Excel工作表上显示数据。 在这两种情况下，都可以将数据元素拖动到Excel工作表。 这两种方法都创建通过 绑定到数据源（如 或 Web 服务 <xref:System.Windows.Forms.BindingSource> ） <xref:System.Data.DataSet> 的数据的控件。

> [!NOTE]
> 将重复架构元素映射到工作表时，Visual Studio创建 <xref:Microsoft.Office.Tools.Excel.ListObject> 。 <xref:Microsoft.Office.Tools.Excel.ListObject>不会通过 自动绑定到数据 <xref:System.Windows.Forms.BindingSource> 。 必须通过在"属性"窗口中设置 和 属性，手动 <xref:Microsoft.Office.Tools.Excel.ListObject> <xref:System.Windows.Forms.BindingSource.DataSource%2A> 将 <xref:System.Windows.Forms.BindingSource.DataMember%2A> 绑定到数据源。

 下表显示了这两种方法之间的一些差异。

|XML 架构|“数据源”窗口|
|----------------|-------------------------|
|使用Office接口。|使用 **"数据源**"窗口Visual Studio。|
|启用用于从 XML Office导入和导出数据的内置功能。|必须以编程方式提供导入和导出功能。|
|必须编写代码以使用数据填充生成的控件。|从"数据源 **"窗口添加的** 控件会自动生成代码来填充这些控件，以及使用数据库服务器时所需的连接字符串。|

## <a name="behavior-when-schemas-are-attached-to-word-documents"></a>架构附加到 Word 文档时的行为
 将架构附加到文档级项目中使用的 Word 文档时，不会创建Office对象。 但是，将架构元素映射到文档时，会创建控件。 控件的类型取决于映射的元素类型;重复元素生成 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件，非重复元素生成 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件。 有关详细信息，请参阅 [XMLNodes 控件和](../vsto/xmlnodes-control.md) [XMLNode 控件](../vsto/xmlnode-control.md)。

## <a name="deployment-of-solutions-that-include-xml-schemas"></a>部署包含 XML 架构的解决方案
 应创建一个安装程序来部署使用映射到文档的 XML 架构的解决方案。 安装程序应在用户计算机的架构库中注册架构。 如果不注册架构，解决方案仍将正常工作，因为 Word 基于用户打开文档时文档中的元素生成临时架构。 但是，用户将无法针对或保存用于创建项目的架构执行验证。 有关安装程序的信息，请参阅 [部署应用程序、服务和组件](../deployment/deploying-applications-services-and-components.md)。

 还可以向项目添加代码，以检查架构是否在库中并注册。 如果不是，可以警告用户。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataWordVB/ThisDocument.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataWordCS/ThisDocument.cs" id="Snippet1":::

## <a name="see-also"></a>另请参阅

- [如何：将架构映射到文档中的 Word Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [如何：将架构映射到 Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
