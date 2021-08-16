---
title: 在窗体间传递数据
description: 在此Windows窗体控件演练中，获取有关将数据从一个窗体传递到另一个窗体的分步说明。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- walkthroughs [Windows Forms], data
- walkthroughs [Visual Studio], data
- data [Visual Studio], passing between forms
- forms, passing data between
- Windows Forms, walkthroughs
ms.assetid: 78bf038b-9296-4fbf-b0e8-d881d1aff0df
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 6e6fff43784338d52abecf29e889aafdc095c80771683656a11670f37ed6fa28
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121347007"
---
# <a name="pass-data-between-forms"></a>在窗体间传递数据

本演练提供了有关将数据从一个窗体传递到另一个窗体的分步说明。 使用 Northwind 中的客户和订单表，一个窗体允许用户选择客户，另一个窗体显示所选客户的订单。 本演练演示如何在接收来自第一个窗体的数据的第二个窗体上创建方法。

> [!NOTE]
> 本演练仅演示在窗体之间传递数据的一种方法。 还有其他选项可用于将数据传递到窗体，包括创建第二个构造函数来接收数据，或创建可以使用第一个窗体的数据设置的公共属性。

本演练涉及以下任务：

- 创建新的 Windows **窗体应用程序** 项目。

- 使用数据源配置向导 创建 [和配置数据集](../data-tools/media/data-source-configuration-wizard.png)。

- 选择从“数据源”窗口拖动某些项时要在窗体上创建的控件。 有关详细信息，请参阅设置从"数据源"窗口拖动时 [要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

- 通过将某些项从“数据源”窗口拖到窗体上来创建数据绑定控件。

- 创建具有网格的第二个窗体来显示数据。

- 创建一个 TableAdapter 查询来获取特定客户的订单。

- 在窗体间传递数据。

## <a name="prerequisites"></a>必备条件

本演练使用 SQL Server Express LocalDB和 Northwind 示例数据库。

1. 如果尚未安装SQL Server Express LocalDB，请从下载页SQL Server Express安装它，或者通过 [](https://www.microsoft.com/sql-server/sql-server-editions-express)**Visual Studio 安装程序。** 在Visual Studio 安装程序中，SQL Server Express LocalDB可以安装为数据存储和处理工作负荷的一部分，也可以作为单个组件进行安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在Visual Studio中，**打开SQL Server 对象资源管理器窗口**。  (SQL Server 对象资源管理器作为数据存储和处理工作负荷的一部分安装在Visual Studio 安装程序.) 展开 **SQL Server节点。** 右键单击实例LocalDB并选择"新建 **查询"。**

       查询编辑器窗口随即打开。

    2. 将[Northwind Transact-SQL脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL脚本从头开始创建 Northwind 数据库，并使用数据填充该数据库。

    3. 将 T-SQL脚本粘贴到查询编辑器中，然后选择"执行 **"** 按钮。

       短时间后，查询完成运行，并创建 Northwind 数据库。

## <a name="create-the-windows-forms-app-project"></a>创建 Windows Forms 应用项目

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 展开左侧 **窗格中Visual Basic"Visual C#"** 或"Windows"。 

3. 在中间窗格中，选择"Windows **窗体应用"** 项目类型。

4. 将项目命名 **PassingDataBetweenForms**，然后选择"确定 **"。**

     创建“PassingDataBetweenForms”项目并添加到“解决方案资源管理器”中。

## <a name="create-the-data-source"></a>创建数据源

1. 若要打开"**数据源"** 窗口，请在"数据 **"** 菜单上单击"**显示数据源"。**

2. 在" **数据源"** 窗口中， **选择"添加新数据源** "以启动 **"数据源配置"** 向导。

3. 在 **“选择数据源类型”** 页上选择 **“数据库”** ，然后单击 **“下一步”**。

4. 在“选择数据库模型”页面上，确认已指定“数据集”，然后单击“下一步”。

5. 在 **"选择数据连接"** 页上，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

    - 选择“新建连接”以启动“添加/修改连接”对话框。

6. 如果数据库需要密码并且已启用含有敏感数据的选项，请选择该选项，然后单击“下一步”。

7. 在"**将连接字符串保存到应用程序配置文件"页上**，单击"下一 **步"。**

8. 在“选择数据库对象”页上，展开“表”节点。

9. 选择“Customers”和“Orders”表，然后单击“完成”。

     将“NorthwindDataSet”添加到项目中，然后“数据源”窗口中将显示“Customers”和“Orders”表。

## <a name="create-the-first-form-form1"></a>在 Form1 窗体 (窗体) 

通过将“Customers”节点从“数据源”窗口拖到窗体上，可以创建数据绑定网格（<xref:System.Windows.Forms.DataGridView> 控件）。

### <a name="to-create-a-data-bound-grid-on-the-form"></a>在窗体上创建数据绑定网格

- 将主“Customers”节点从“数据源”窗口拖到“Form1”上。

     “Form1”上显示用于导航记录的 <xref:System.Windows.Forms.DataGridView> 和工具栏 (<xref:System.Windows.Forms.BindingNavigator>)。 组件栏中显示[“NorthwindDataSet”](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

## <a name="create-the-second-form"></a>创建第二个窗体

创建要将数据传递到的第二个窗体。

1. 从“项目”菜单中，选择“添加 Windows 窗体”。

2. 保留“Form2”的默认名称，然后单击“添加”。

3. 将主“Orders”节点从“数据源”窗口拖到“Form2”上。

     “Form2”上显示用于导航记录的 <xref:System.Windows.Forms.DataGridView> 和工具栏 (<xref:System.Windows.Forms.BindingNavigator>)。 组件栏中显示[“NorthwindDataSet”](../data-tools/dataset-tools-in-visual-studio.md)、CustomersTableAdapter、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

4. 从组件栏删除“OrdersBindingNavigator”。

     “OrdersBindingNavigator”从“Form2”中消失。

## <a name="add-a-tableadapter-query"></a>添加 TableAdapter 查询

将 TableAdapter 查询添加到 Form2，以在 Form1 上加载所选客户的订单。

1. 双击“解决方案资源管理器”中的“NorthwindDataSet.xsd”文件。

2. 右键单击“OrdersTableAdapter”，然后选择“添加查询”。

3. 保留“使用 SQL 语句”的默认选项，然后单击“下一步”。

4. 保留“选择返回行”的默认选项，然后单击“下一步”。

5. 向查询添加 WHERE 子句，根据 `CustomerID` 返回 `Orders`。 查询应当类似于：

    ```sql
    SELECT OrderID, CustomerID, EmployeeID, OrderDate, RequiredDate, ShippedDate, ShipVia, Freight, ShipName, ShipAddress, ShipCity, ShipRegion, ShipPostalCode, ShipCountry
    FROM Orders
    WHERE CustomerID = @CustomerID
    ```

    > [!NOTE]
    > 验证数据库的参数语法是否正确。 例如，在 Microsoft Access 中，WHERE 子句应当如下：`WHERE CustomerID = ?`。

6. 单击“下一步”。

7. 对于" **填充 DataTableMethod 名称"，** 请键入 `FillByCustomerID` 。

8. 清除“返回 DataTable”选项，然后单击“下一步”。

9. 单击“完成”。

## <a name="create-a-method-on-form2-to-pass-data-to"></a>在 Form2 上创建一个将数据传递到的方法

1. 右键单击“Form2”，然后选择“查看代码”，在“代码编辑器”中打开“Form2”。

2. 使用 `Form2_Load` 方法后，将以下代码添加到“Form2”：

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form2.vb" id="Snippet1":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form2.cs" id="Snippet1":::

## <a name="create-a-method-on-form1-to-pass-data-and-display-form2"></a>在 Form1 上创建方法以传递数据和显示 Form2

1. 在“Form1”中，右键单击“Customer”数据网格，然后单击“属性”。

2. 在“属性”窗口中，单击“事件”。

3. 双击“CellDoubleClick”事件。

     将显示代码编辑器。

4. 更新方法定义以匹配以下示例：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs" id="Snippet2":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb" id="Snippet2":::

## <a name="run-the-app"></a>运行应用

- 按 **F5** 运行该应用程序。

- 双击“Form1”中的客户记录，打开包含该客户订单的“Form2”。

## <a name="next-steps"></a>后续步骤

根据应用程序的需求，在窗体间传递数据之后可能还需要执行一些步骤。 你可以通过以下操作来增强此演练的效果：

- 编辑数据集来添加或移除数据库对象。 有关详细信息，请参阅[创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)。

- 添加将数据保存回数据库的功能。 有关详细信息，请参阅 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
