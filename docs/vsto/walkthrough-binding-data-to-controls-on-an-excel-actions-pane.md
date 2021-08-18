---
title: 演练：将数据绑定到"操作"窗格中Excel控件
description: 将数据绑定到操作窗格中的控件，Microsoft Excel。 控件演示 SQL Server 数据库中表之间的主/从关系。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], data binding
- actions panes [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], smart documents
- data binding [Office development in Visual Studio], actions panes
- actions panes [Office development in Visual Studio], binding controls
- smart documents [Office development in Visual Studio], data binding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 7a6a6a914c1777142a1febefa12c0c78bbcb290d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122099342"
---
# <a name="walkthrough-bind-data-to-controls-on-an-excel-actions-pane"></a>演练：将数据绑定到"操作"窗格中Excel控件
  本演练演示了数据绑定到操作窗格中控件的数据Microsoft Office Excel。 控件演示 SQL Server 数据库中表之间的主/从关系。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 本演练演示以下任务：

- 将控件添加到工作表。

- 创建操作窗格控件。

- 向操作窗格控件Windows窗体控件添加数据绑定。

- 在应用程序打开时显示操作窗格。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] 或 [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)]。

- 使用 Northwind 数据库访问SQL Server示例数据库。

- 从数据库读取和写入数据库SQL Server的权限。

## <a name="create-the-project"></a>创建项目
 第一步是创建一个 Excel 工作簿项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一Excel工作簿项目，其名称为 **"我的Excel操作窗格"。** 在向导中，选择 **"创建新文档"。** 有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     Visual Studio设计器中打开新的 Excel 工作簿，并将"我的Excel **操作窗格**"项目添加到 **解决方案资源管理器。**

## <a name="add-a-new-data-source-to-the-project"></a>向项目添加新数据源

### <a name="to-add-a-new-data-source-to-the-project"></a>向项目添加新数据源

1. 如果 **"数据源"** 窗口不可见，请通过选择菜单栏上的"查看其他数据源"Windows  >    >  **显示它**。

2. 选择 **“添加新数据源”** 以启动 **“数据源配置向导”**。

3. 选择"**数据库**"，然后单击"下一 **步"。**

4. 选择与 Northwind 示例数据库SQL Server连接，或者使用"新建连接"按钮 **添加新** 连接。

5. 单击“下一步”。

6. 清除选项以保存连接（如果已选中）并单击"下一步 **"。**

7. 展开" **数据库对象** "窗口中的 **"表"** 节点。

8. 选中 **"Suppliers"表旁边的** 复选框。

9. 展开 **"Products"** 表，然后选择"ProductName"、SupplierID、QuantityPerUnit 和 **UnitPrice**。  

10. 单击“完成”。

    向导将 **Suppliers 表** 和 **Products** 表添加到 **"数据源"** 窗口。 它还会将类型数据集添加到项目中，该数据集在 **解决方案资源管理器。**

## <a name="add-controls-to-the-worksheet"></a>将控件添加到工作表
 接下来，将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件和 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加到第一个工作表。

### <a name="to-add-a-namedrange-control-and-a-listobject-control"></a>添加 NamedRange 控件和 ListObject 控件

1. 验证"**我的Excel操作Pane.xlsx** 工作簿是否打开，并显示Visual Studio设计器 `Sheet1` 。

2. 在" **数据源"** 窗口中，展开 **"Suppliers"** 表。

3. 单击"公司名称"节点上的下 **拉箭头，** 然后单击 **"NamedRange"。**

4. 将 **"公司名称**"从 **"数据源"窗口** 拖到 **中的单元格 A2。** `Sheet1`

     将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 创建名为 `CompanyNameNamedRange` 的控件，文本 \<CompanyName> 将显示在单元格 **A2 中**。 同时，将 <xref:System.Windows.Forms.BindingSource> 名为 的 `suppliersBindingSource` 、表适配器和 <xref:System.Data.DataSet> 添加到项目中。 控件绑定到 <xref:System.Windows.Forms.BindingSource> ，而该控件又绑定到 <xref:System.Data.DataSet> 实例。

5. 在 **"数据源"** 窗口中，向下滚动"Suppliers"表 **下的** 列。 列表底部是 Products **表;** 它在此处是因为它是 **Suppliers** 表的子级。 选择 **此 Products** 表，而不是与 **Suppliers** 表处于同一级别的表，然后单击出现的下拉箭头。

6. 单击 **下拉列表中的 ListObject，** 然后将 **Products** 表拖到 **中的单元格 A6。** `Sheet1`

     在 <xref:Microsoft.Office.Tools.Excel.ListObject> 单元格 `ProductNameListObject` **A6** 中创建名为 的控件。 同时，命名 <xref:System.Windows.Forms.BindingSource> `productsBindingSource` 的 和表适配器将添加到项目中。 控件绑定到 <xref:System.Windows.Forms.BindingSource> ，而该控件又绑定到 <xref:System.Data.DataSet> 实例。

7. 仅对于 C#，请选择组件托盘上的 **suppliersBindingSource，** 在"属性"窗口中将 **"修饰** 符"**属性更改为"内部**"。

## <a name="add-controls-to-the-actions-pane"></a>将控件添加到操作窗格
 接下来，需要一个包含组合框的操作窗格控件。

### <a name="to-add-an-actions-pane-control"></a>添加操作窗格控件

1. 在 中 **Excel"我的操作"** 窗格 **解决方案资源管理器。**

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在"**添加新项"对话框中**，选择"**操作窗格控件**"，将其命名 **为"ActionsControl"，** 然后单击"添加 **"。**

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>向操作窗格控件Windows窗体控件添加数据绑定

1. 从" **工具箱"的** "公共控件 **"** 选项卡中， <xref:System.Windows.Forms.ComboBox> 将控件拖动到操作窗格控件。

2. 将 Size **属性** 更改为 **171， 21**。

3. 调整用户控件的大小以适应组合框。

## <a name="bind-the-control-on-the-actions-pane-to-data"></a>将操作窗格上的控件绑定到数据
 在本部分，你将将 的数据源设置为与工作表上的 控件 <xref:System.Windows.Forms.ComboBox> <xref:Microsoft.Office.Tools.Excel.NamedRange> 相同的数据源。

### <a name="to-set-data-binding-properties-of-the-control"></a>设置控件的数据绑定属性

1. 右键单击操作窗格控件，然后单击"**查看代码"。**

2. 将以下代码添加到 <xref:System.Windows.Forms.UserControl.Load> 操作窗格控件的 事件。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ActionsControl.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs" id="Snippet1":::

3. 在 C# 中，必须为 创建事件处理程序 `ActionsControl` 。 可以将此代码放在构造函数 `ActionsControl` 中。 有关创建事件处理程序的信息，请参阅如何：在项目中创建[Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs" id="Snippet2":::

## <a name="show-the-actions-pane"></a>显示操作窗格
 在运行时添加 控件之前，操作窗格不可见。

#### <a name="to-show-the-actions-pane"></a>显示操作窗格

1. 在 **解决方案资源管理器** 中，右键单击 *ThisWorkbook.vb* 或 *ThisWorkbook.cs，* 然后单击"**查看代码"。**

2. 在 类中创建用户控件的新 `ThisWorkbook` 实例。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet3":::

3. 在 <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> 的事件处理程序 `ThisWorkbook` 中，将 控件添加到操作窗格。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet4":::

## <a name="test-the-application"></a>测试应用程序
 现在，可以测试文档，以验证打开文档时操作窗格是否打开，以及控件是否具有主/详细信息关系。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 确认操作窗格可见。

3. 在列表框中选择一家公司。 验证控件中是否列出了公司名称，以及 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件中是否列出了产品 <xref:Microsoft.Office.Tools.Excel.ListObject> 详细信息。

4. 选择各种公司以验证公司名称和产品详细信息是否相应更改。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 将数据绑定到 Word 中的控件。 有关详细信息，请参阅 [演练：将数据绑定到 Word](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)操作窗格上的控件。

- 部署项目。 有关详细信息，请参阅使用[Office 部署 ClickOnce。](../vsto/deploying-an-office-solution-by-using-clickonce.md)

## <a name="see-also"></a>请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：管理操作窗格上的控件布局](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
