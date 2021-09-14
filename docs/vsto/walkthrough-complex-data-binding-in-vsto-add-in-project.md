---
title: 演练：外接程序项目中VSTO数据绑定
description: 了解如何将控件添加到Microsoft Excel工作表，并运行时将控件绑定到数据。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], Excel
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 8f9a554d485abf329a5f3a2933f306035cefa27c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664933"
---
# <a name="walkthrough-complex-data-binding-in-vsto-add-in-project"></a>演练：外接程序项目中VSTO数据绑定
  可以将数据绑定到 VSTO 外接程序项目中的宿主控件和 Windows 窗体控件。 本演练演示如何在运行时向 Microsoft Office Excel 工作表中添加控件并将控件绑定到数据。

 [!INCLUDE[appliesto_xlallapp](../vsto/includes/appliesto-xlallapp-md.md)]

 本演练演示以下任务：

- 在运行时将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加到工作表。

- 创建用于将该控件连接到某个数据集实例的 <xref:System.Windows.Forms.BindingSource> 。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 对附加了 `AdventureWorksLT` 示例数据库且正在运行的 SQL Server 2005 或 SQL Server 2005 Express 实例的访问权限。 可以从存储库 `AdventureWorksLT` 的 SQL Server[示例GitHub数据库](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。 有关附加数据库的详细信息，请参阅下列主题：

  - 若要使用 SQL Server Management Studio 或 SQL Server Management Studio Express 附加数据库，请参阅[如何：将数据库附加到 (SQL Server Management Studio) 。 ](/sql/relational-databases/databases/attach-a-database)

  - 若要使用命令行附加数据库，请参阅[如何：将数据库文件附加到 SQL Server Express。](/previous-versions/sql/)

## <a name="create-a-new-project"></a>创建新项目
 第一步是创建 Excel VSTO 外接程序项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 Visual Basic 或 C# 创建一个名为“从数据库填充工作表” 的 Excel VSTO 外接程序项目。

     有关详细信息，请参阅 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio 会打开 `ThisAddIn.vb` 或 `ThisAddIn.cs` 文件，并将“从数据库填充工作表”  项目附加到“解决方案资源管理器” 中。

## <a name="create-a-data-source"></a>创建数据源
 使用 **“数据源”** 窗口将类型化数据集添加到项目中。

### <a name="to-add-a-typed-dataset-to-the-project"></a>向项目中添加类型化数据集

1. 如果"**数据源"** 窗口不可见，请通过选择菜单栏上的"查看其他数据源"Windows  >    >  **显示它**。

2. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”**。

3. 单击“数据库” ，然后单击“下一步” 。

4. 如果已与 `AdventureWorksLT` 数据库建立连接，请选择此连接，然后单击“下一步” 。

    否则，单击“新建连接” ，然后使用“添加连接”  对话框创建新连接。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

5. 在“将连接字符串保存到应用程序配置文件中”  页中，单击“下一步” 。

6. 在“选择数据库对象”  页中展开“表”  ，再选择“Address (SalesLT)” 。

7. 单击“完成”  。

    *AdventureWorksLTDataSet.xsd* 文件 **将添加到** 解决方案资源管理器。 此文件定义以下各项：

   - 一个名为 `AdventureWorksLTDataSet`的类型化数据集。 此数据集表示 AdventureWorksLT 数据库中“Address (SalesLT)”  表的内容。

   - 名为 的 TableAdapter。 `AddressTableAdapter` 此 TableAdapter 可用于读取和写入 中的数据 `AdventureWorksLTDataSet` 。 有关详细信息，请参阅 [TableAdapter 概述](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)。

     在本演练后面的部分中，你将使用这两个对象。

## <a name="create-controls-and-bind-controls-to-data"></a>创建控件，将控件绑定到数据
 对于本演练，只要用户打开工作薄， <xref:Microsoft.Office.Tools.Excel.ListObject> 控件就会在所选表中显示所有数据。 列表对象使用 <xref:System.Windows.Forms.BindingSource> 将控件连接到数据库。

 有关将控件绑定到数据的更多信息，请参阅[将数据绑定到解决方案 Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

### <a name="to-add-the-list-object-dataset-and-table-adapter"></a>添加列表对象、数据集和表适配器

1. 在 `ThisAddIn` 类中，声明以下控件以显示 `Address` 数据集的 `AdventureWorksLTDataSet` 表。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet1":::

2. 在 `ThisAddIn_Startup` 方法中，添加以下代码以初始化数据集，并使用 `AdventureWorksLTDataSet` 数据集的信息来填充此数据集。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet2":::

3. 将以下代码添加到 `ThisAddIn_Startup` 方法中。 这会生成一个可扩展工作表的宿主项。 有关详细信息，请参阅扩展[Word 文档和Excel运行时VSTO外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet3":::

4. 创建一个范围并添加 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet4":::

5. 使用 `AdventureWorksLTDataSet` 将列表对象绑定到 <xref:System.Windows.Forms.BindingSource>。 传入你想要绑定到列表对象的列的名称。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet5":::

## <a name="test-the-add-in"></a>测试外接程序
 打开 Excel 时， <xref:Microsoft.Office.Tools.Excel.ListObject> 会显示来自 `Address` 数据集的 `AdventureWorksLTDataSet` 表的数据。

### <a name="to-test-the-vsto-add-in"></a>若要测试 VSTO 外接程序

- 按 **F5**。

     已在工作表中创建了一个名为 <xref:Microsoft.Office.Tools.Excel.ListObject> 的 `addressListObject` 控件。 同时，向项目添加了一个名为 `adventureWorksLTDataSet` 的数据集对象和一个名为 <xref:System.Windows.Forms.BindingSource> 的 `addressBindingSource` 。 已将 <xref:Microsoft.Office.Tools.Excel.ListObject> 绑定到 <xref:System.Windows.Forms.BindingSource>，而后者又绑定到该数据集对象。

## <a name="see-also"></a>另请参阅

- [解决方案Office数据](../vsto/data-in-office-solutions.md)
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [如何：使用数据库中的数据填充工作表](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [如何：使用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [如何：使用服务数据填充文档](../vsto/how-to-populate-documents-with-data-from-services.md)
- [如何：使用 对象的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [如何：在工作表中滚动浏览数据库记录](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)
- [如何：使用来自主机控件的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [演练：文档级项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
- [演练：文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
- [在解决方案中Office数据库文件概述](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [添加新数据源](../data-tools/add-new-data-sources.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [在解决方案中Office数据库文件概述](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)
