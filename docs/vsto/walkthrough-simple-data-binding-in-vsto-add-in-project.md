---
title: 演练：在外接程序项目中VSTO数据绑定
description: 了解如何向文档添加控件Microsoft Word控件并运行时将控件绑定到数据。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- data binding [Office development in Visual Studio], Word
- data [Office development in Visual Studio], simple binding data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 10ecb5b04198a0937b06876760862c7b9cf415c0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155431"
---
# <a name="walkthrough-simple-data-binding-in-vsto-add-in-project"></a>演练：在外接程序中VSTO数据绑定Project

可以将数据绑定到 VSTO 外接程序项目中的宿主控件和 Windows 窗体控件。 本演练演示如何在运行时向 Microsoft Office Word 文档中添加控件并将控件绑定到数据。

[!INCLUDE[appliesto_wdallapp](../vsto/includes/appliesto-wdallapp-md.md)]

本演练演示以下任务：

- 在运行时向文档中添加 <xref:Microsoft.Office.Tools.Word.ContentControl> 。

- 创建用于将该控件连接到某个数据集实例的 <xref:System.Windows.Forms.BindingSource> 。

- 使用户可以滚动浏览记录以及在控件中查看记录。

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件

您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

- 对附加了 `AdventureWorksLT` 示例数据库且正在运行的 SQL Server 2005 或 SQL Server 2005 Express 实例的访问权限。 可以从存储库 `AdventureWorksLT` 的 SQL Server[示例GitHub数据库](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)。 有关附加数据库的详细信息，请参阅下列主题：

  - 若要使用 SQL Server Management Studio 或 SQL Server Management Studio Express 附加数据库，请参阅如何：将数据库附加到[ (SQL Server Management Studio) 。 ](/sql/relational-databases/databases/attach-a-database)

  - 若要使用命令行附加数据库，请参阅[如何：将数据库文件附加到 SQL Server Express。](/previous-versions/sql/)

## <a name="create-a-new-project"></a>创建新项目

第一步是创建 Word VSTO 外接程序项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 Visual Basic 或 C# 创建一个名为“从数据库填充文档” 的 Word VSTO 外接程序项目。

     有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     Visual Studio *ThisAddIn.vb* 或 *ThisAddIn.cs* 文件，并将从数据库项目填充文档添加到 **解决方案资源管理器。**

2. 如果项目面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] ，请添加对程序集Microsoft.Office.Tools.Word.v4.0.Utilities.dll引用。 在本演练后面的部分中，需要此引用才能以编程方式向文档中添加 Windows 窗体控件。

## <a name="create-a-data-source"></a>创建数据源

使用 **“数据源”** 窗口将类型化数据集添加到项目中。

### <a name="to-add-a-typed-dataset-to-the-project"></a>向项目中添加类型化数据集

1. 如果"**数据源"** 窗口不可见，请通过选择菜单栏上的"查看其他数据源"Windows  >    >  **显示它**。

2. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”**。

3. 单击“数据库” ，然后单击“下一步” 。

4. 如果已与 `AdventureWorksLT` 数据库建立连接，请选择此连接，然后单击“下一步” 。

    否则，单击“新建连接” ，然后使用“添加连接”  对话框创建新连接。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

5. 在“将连接字符串保存到应用程序配置文件中”  页中，单击“下一步” 。

6. 在“选择数据库对象”  页中展开“表”  ，再选择“Customer (SalesLT)” 。

7. 单击“完成”。

    *AdventureWorksLTDataSet.xsd* 文件将添加到 **解决方案资源管理器。** 此文件定义以下各项：

   - 一个名为 `AdventureWorksLTDataSet`的类型化数据集。 此数据集表示 AdventureWorksLT 数据库中的“Customer (SalesLT)”  表的内容。

   - 名为 的 TableAdapter。 `CustomerTableAdapter` 此 TableAdapter 可用于读取和写入 中的数据 `AdventureWorksLTDataSet` 。 有关详细信息，请参阅 [TableAdapter 概述](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)。

     在本演练后面的部分中，你将使用这两个对象。

## <a name="create-controls-and-binding-controls-to-data"></a>创建控件和将控件绑定到数据

本演练中用于查看数据库记录的接口是基本的，它是在文档内部创建的。 一个 <xref:Microsoft.Office.Tools.Word.ContentControl> 一次显示一条数据库记录，两个 <xref:Microsoft.Office.Tools.Word.Controls.Button> 控件允许你以前后滚动的方式查看记录。 该内容控件使用 <xref:System.Windows.Forms.BindingSource> 来连接到数据库。

有关将控件绑定到数据的更多信息，请参阅将数据绑定到 Office[解决方案 中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

### <a name="to-create-the-interface-in-the-document"></a>在文档中创建界面

1. 在 `ThisAddIn` 类中声明下列控件，以显示和滚动查看 `Customer` 数据库的 `AdventureWorksLTDataSet` 表。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet1":::

2. 在 `ThisAddIn_Startup` 方法中添加下面的代码，以便初始化数据集并使用 `AdventureWorksLTDataSet` 数据库中的信息填充数据集。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet2":::

3. 将以下代码添加到 `ThisAddIn_Startup` 方法中。 这会生成一个扩展文档的宿主项。 有关详细信息，请参阅扩展[Word 文档和Excel运行时VSTO外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet3":::

4. 在文档开始处定义多个范围。 这些范围标识用于插入文本和放置控件的位置。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet4":::

5. 将界面控件添加到前面定义的范围内。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet5":::

6. 使用 `AdventureWorksLTDataSet` 将内容控件绑定到 <xref:System.Windows.Forms.BindingSource>。 对于 C# 开发人员，为 <xref:Microsoft.Office.Tools.Word.Controls.Button> 控件添加两个事件处理程序。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet6":::

7. 添加下面的代码，以浏览数据库记录。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet7":::

## <a name="test-the-add-in"></a>测试外接程序

打开 Word 后，内容控件随即显示 `AdventureWorksLTDataSet` 数据集中的数据。 通过单击“下一条”  和“上一条”  按钮来滚动查看数据库记录。

### <a name="to-test-the-vsto-add-in"></a>若要测试 VSTO 外接程序

1. 按 **F5**。

     即会创建一个名为 `customerContentControl` 的内容控件，并向该控件填充数据。 同时，向项目添加了一个名为 `adventureWorksLTDataSet` 的数据集对象和一个名为 <xref:System.Windows.Forms.BindingSource> 的 `customerBindingSource` 。 已将 <xref:Microsoft.Office.Tools.Word.ContentControl> 绑定到 <xref:System.Windows.Forms.BindingSource>，而后者又绑定到该数据集对象。

2. 单击“下一条”  和“上一条”  按钮来滚动查看数据库记录。

## <a name="see-also"></a>请参阅

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
- [如何：使用 对象的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [如何：使用来自主机控件的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [在解决方案中Office数据库文件概述](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)
