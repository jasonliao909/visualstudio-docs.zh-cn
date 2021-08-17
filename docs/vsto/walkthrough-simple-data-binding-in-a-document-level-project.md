---
title: 演练：文档级项目中的简单数据绑定
description: 了解文档级项目中数据绑定的基础知识，以及 SQL Server 数据库中的单个数据字段绑定到 Microsoft Excel。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], worksheet cell to Database field
- worksheets [Office development in Visual Studio], binding worksheet cell to Database field
- Database field [Office development in Visual Studio]
- data [Office development in Visual Studio], binding data
- simple data binding [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: c965b63c4f7aec8229fce45be95b5b7c74bd0c96
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122025456"
---
# <a name="walkthrough-simple-data-binding-in-a-document-level-project"></a>演练：文档级项目中的简单数据绑定
  本演练演示文档级项目中数据绑定的基础知识。 数据库的单个数据SQL Server绑定到数据库中命名Microsoft Office Excel。 本演练还演示如何添加控件，使你可以滚动浏览表中的所有记录。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练演示以下任务：

- 为项目创建Excel数据源。

- 将控件添加到工作表。

- 滚动浏览数据库记录。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 使用 Northwind 数据库访问SQL Server示例数据库。

- 从数据库读取和写入数据库SQL Server的权限。

## <a name="create-a-new-project"></a>创建新项目
 在此步骤中，你将创建一个Excel工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 Excel C# 创建一个名称为"我的简单数据绑定"Visual Basic工作簿项目。 确保已 **选择"创建新** 文档"。 有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

   Visual Studio设计器中打开新的 Excel 工作簿，并将"**我的简单** 数据绑定"项目添加到 **解决方案资源管理器。**

## <a name="create-the-data-source"></a>创建数据源
 使用 **“数据源”** 窗口将类型化数据集添加到项目中。

### <a name="to-create-the-data-source"></a>创建数据源

1. 如果"**数据源"** 窗口不可见，请通过选择菜单栏上的"查看其他数据源"Windows  >    >  **显示它**。

2. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”**。

3. 选择"**数据库**"，然后单击"下一 **步"。**

4. 选择与 Northwind 示例数据库SQL Server连接，或者使用"新建连接"按钮 **添加新** 连接。

5. 选择或创建连接后，单击"下一 **步"。**

6. 清除该选项以保存连接（如果已选中）并单击"下一步 **"。**

7. 展开" **数据库对象** "窗口中的 **"表"** 节点。

8. 选中"Customers"表 **旁边的** 复选框。

9. 单击“完成”。

   向导将 **Customers 表** 添加到 **"数据源"** 窗口。 它还会将类型数据集添加到项目中，该数据集在 **解决方案资源管理器。**

## <a name="add-controls-to-the-worksheet"></a>将控件添加到工作表
 对于本演练，需要第一个工作表上两个命名范围和四个按钮。 首先，从"数据源"窗口添加两个 **命名范围，** 以便它们自动绑定到数据源。 接下来，添加"工具箱"中的 **按钮**。

### <a name="to-add-two-named-ranges"></a>添加两个命名范围

1. 验证"*我的简单数据Binding.xlsx* 工作簿在设计器中是否Visual Studio，并显示 **Sheet1。**

2. 打开" **数据源"** 窗口并展开" **客户"** 节点。

3. 选择 **"CompanyName"** 列，然后单击出现的下拉箭头。

4. 在 **下拉列表中选择"NamedRange"，** 然后将 **"CompanyName"** 列拖到 **单元格 A1 中**。

     在 <xref:Microsoft.Office.Tools.Excel.NamedRange> 单元格 `companyNameNamedRange` **A1** 中创建名为 的控件。 同时，将 <xref:System.Windows.Forms.BindingSource> 名为 `customersBindingSource` 、表适配器和 实例的 添加到 <xref:System.Data.DataSet> 项目中。 控件绑定到 <xref:System.Windows.Forms.BindingSource> ，而该控件又绑定到 <xref:System.Data.DataSet> 实例。

5. 在"**数据源"窗口中选择"CustomerID"****列，** 然后单击出现的下拉箭头。

6. 单击 **下拉列表中的 NamedRange，** 然后将 **CustomerID** 列拖到 **单元格 B1 。**

7. 另 <xref:Microsoft.Office.Tools.Excel.NamedRange> 一个名为 `customerIDNamedRange` 的控件在 **单元格 B1** 中创建，并绑定到 <xref:System.Windows.Forms.BindingSource> 。

### <a name="to-add-four-buttons"></a>添加四个按钮

1. 从" **工具箱"的** "公共控件 **"选项卡中**，向 <xref:System.Windows.Forms.Button> **工作表的单元格 A3 添加** 控件。

    此按钮名为 `Button1` 。

2. 按此顺序向以下单元格再添加三个按钮，以便按如下所示显示名称：

   |单元|(名称)|
   |----------|--------------|
   |B3|Button2|
   |C3|Button3|
   |D3|Button4|

   下一步是向按钮添加文本，在 C# 中添加事件处理程序。

## <a name="initialize-the-controls"></a>初始化控件
 设置按钮文本，并添加事件期间 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 的事件处理程序。

### <a name="to-initialize-the-controls"></a>初始化控件

1. 在 **解决方案资源管理器** 中，右键单击 **"Sheet1.vb"** 或 **"Sheet1.cs"，** 然后单击快捷菜单上的"查看代码"。 

2. 将以下代码添加到 `Sheet1_Startup` 方法，以设置每个按钮的文本。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet2":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet2":::

3. 仅对于 C#，向 方法添加按钮单击事件的事件 `Sheet1_Startup` 处理程序。

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet3":::

   现在添加代码来处理按钮 <xref:System.Windows.Forms.Control.Click> 的事件，以便用户可以浏览记录。

## <a name="add-code-to-enable-scrolling-through-the-records"></a>添加代码以启用滚动记录
 将代码添加到 <xref:System.Windows.Forms.Control.Click> 每个按钮的事件处理程序，以在记录中移动。

### <a name="to-move-to-the-first-record"></a>移动到第一条记录

1. 为按钮的 事件 <xref:System.Windows.Forms.Control.Click> 添加事件 `Button1` 处理程序，并添加以下代码以移动到第一条记录：

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet4":::

### <a name="to-move-to-the-previous-record"></a>移动到上一条记录

1. 为按钮的 事件添加事件处理程序，并添加以下代码将位置 <xref:System.Windows.Forms.Control.Click> `Button2` 移回一个：

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet5":::

### <a name="to-move-to-the-next-record"></a>移动到下一条记录

1. 为按钮的 事件添加事件处理程序，并添加以下代码以 <xref:System.Windows.Forms.Control.Click> `Button3` 将位置前进 1：

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet6":::

### <a name="to-move-to-the-last-record"></a>移动到最后一条记录

1. 为按钮的 <xref:System.Windows.Forms.Control.Click> 事件添加事件处理程序，并添加 `Button4` 以下代码以移动到最后一条记录：

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet7":::

## <a name="test-the-application"></a>测试应用程序
 现在，可以测试工作簿，以确保可以浏览数据库中的记录。

### <a name="to-test-your-workbook"></a>测试工作簿

1. 按 **F5** 运行项目。

2. 确认第一条记录出现在单元格 **A1 和** **B1 中**。

3. 单击 **>** `Button3` () 按钮，并确认下一条记录显示在 **单元格 A1** 和 **B1 中**。

4. 单击其他滚动按钮以确认记录按预期更改。

## <a name="next-steps"></a>后续步骤
 本演练演示了将命名范围绑定到数据库中的字段的基础知识。 以下是接下来可能要执行的一些任务：

- 缓存数据，以便可以脱机使用。 有关详细信息，请参阅 [如何：缓存数据以脱机或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- 将单元格绑定到表中的多个列，而不是绑定到一个字段。 有关详细信息，请参阅 [演练：文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)。

- 使用 <xref:System.Windows.Forms.BindingNavigator> 控件滚动记录。 有关详细信息，请参阅[如何：使用窗体 BindingNavigator Windows导航数据](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)。

## <a name="see-also"></a>请参阅
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [解决方案Office数据](../vsto/data-in-office-solutions.md)
- [演练：文档级项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
