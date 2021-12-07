---
title: 演练：在事务中保存数据
description: 本演练介绍如何在 Visual Studio 中使用 System.Transactions 命名空间在事务中保存数据。
ms.custom: SEO-VS-2020
ms.date: 09/08/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System.Transactions namespace
- data [Visual Studio], saving in a transaction
- transactions, saving data
- Transactions namespace
- saving data
ms.assetid: 80260118-08bc-4b37-bfe5-9422ee7a1e4e
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 223a5985a34f5063eacfcd0125b624a09520e6fb
ms.sourcegitcommit: 7a300823cf1bd3355be03bde561cf2777bc09eae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2021
ms.locfileid: "133978454"
---
# <a name="walkthrough-save-data-in-a-transaction"></a>演练：在事务中保存数据

本演练演示如何使用 <xref:System.Transactions> 命名空间在事务中保存数据。 本演练将创建一个 Windows 窗体应用程序。 你将使用“数据源配置”向导为 Northwind 示例数据库中的两个表创建一个数据集。 将数据绑定控件添加到 Windows 窗体，并修改 BindingNavigator 的保存按钮的代码以更新 TransactionScope 内的数据库。

## <a name="prerequisites"></a>先决条件

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果尚未安装 SQL Server Express LocalDB，可以从 [SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过 Visual Studio 安装程序安装。 在 Visual Studio 安装程序中，可以将 SQL Server Express LocalDB 作为 .NET 桌面开发工作负载的一部分或作为单个组件进行安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开“SQL Server 对象资源管理器”窗口。 （在 Visual Studio 安装程序中 SQL Server 对象资源管理器作为数据存储和处理工作负载的一部分安装。）展开 SQL Server 节点 。 右键单击 LocalDB 实例并选择“新建查询”。

       此时将打开查询编辑器窗口。

    2. 将 [Northwind Transact-SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/main/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL 脚本从头开始创建 Northwind 数据库并用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器中，然后选择“执行”按钮。

       不久后，查询完成运行并且 Northwind 数据库创建完成。

## <a name="create-a-windows-forms-application"></a>创建 Windows 窗体应用程序

第一步是创建“Windows 窗体应用程序”。

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 在左侧窗格中展开“Visual C#”或“Visual Basic”，然后选择“Windows 桌面”  。

3. 在中间窗格中，选择“Windows 窗体应用”项目类型。

4. 将项目命名为 SavingDataInATransactionWalkthrough，然后选择“确定” 。

     创建“SavingDataInATransactionWalkthrough”项目并将其添加到“解决方案资源管理器”中。

## <a name="create-a-database-data-source"></a>创建数据库数据源

此步骤根据 Northwind 示例数据库中的 `Customers` 和 `Orders` 表，使用“数据源配置”向导创建数据源。

1. 若要打开“数据源”窗口，在“数据”菜单上选择“显示数据源”  。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 在“选择数据源类型”屏幕中，选择“数据库”，然后选择“下一步”  。

4. 在“选择数据连接”屏幕中，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

         -或-

    - 选择“新建连接”以启动“添加/修改连接”对话框，并创建到 Northwind 数据库的连接。

5. 如果数据库需要密码，请选择包含敏感数据的选项，再选择“下一步”。

6. 在“将连接字符串保存到应用程序配置文件”屏幕中，选择“下一步” 。

7. 在“选择数据库对象”屏幕中，展开“表”节点 。

8. 选择 `Customers` 和 `Orders` 表，然后选择“完成”。

     将“NorthwindDataSet”添加到项目后，“数据源”窗口即会显示 `Customers` 和 `Orders` 表。

## <a name="add-controls-to-the-form"></a>向窗体添加控件

通过将某些项从“数据源”窗口拖到窗体，可创建数据绑定控件。

1. 在“数据源”窗口中展开“Customers”节点 。

2. 将主“Customers”节点从“数据源”窗口拖到“Form1”上。

   用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 此时组件栏中显示 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、`CustomersTableAdapter`、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

3. 将相关的“Orders”节点（不是主“Orders”节点，而是“Fax”列下面的相关子表节点）拖到“CustomersDataGridView”下面的窗体上   。

   窗体上显示一个 <xref:System.Windows.Forms.DataGridView>。 组件栏中显示 `OrdersTableAdapter` 和 <xref:System.Windows.Forms.BindingSource>。

## <a name="add-a-reference-to-the-systemtransactions-assembly"></a>添加对 System.Transactions 程序集的引用

事务使用 <xref:System.Transactions> 命名空间。 默认情况下，没有添加对 system.transactions 程序集的项目引用，因此你需要手动将其添加。

### <a name="to-add-a-reference-to-the-systemtransactions-dll-file"></a>添加对 System.Transactions DLL 文件的引用

1. 在“项目”菜单中，选择“添加引用”。

2. 选择“System.Transactions”（在“.NET”选项卡上），然后选择“确定”  。

     将“System.Transactions”的引用添加到项目。

## <a name="modify-the-code-in-the-bindingnavigators-saveitem-button"></a>修改 BindingNavigator 的 SaveItem 按钮中的代码

由于第一个表已放置在你的窗体上，因此代码会默认添加到 <xref:System.Windows.Forms.BindingNavigator> 上保存按钮的 `click` 事件中。 你需要手动添加代码以更新所有附加的表。 对于本演练，我们将重构源自保存按钮的单击事件处理程序的现有保存代码。 还将创建更多的方法以根据是需要添加行还是需要删除行提供特定的更新功能。

### <a name="to-modify-the-auto-generated-save-code"></a>修改自动生成的保存代码

1. 在“CustomersBindingNavigator”上选择“保存”按钮（带有软盘图标的按钮） 。

2. 将 `CustomersBindingNavigatorSaveItem_Click` 方法替换为以下代码：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet4":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet4":::

对相关数据的协调更改的顺序如下：

- 删除子记录。 （在此情况下，从 `Orders` 表中删除记录。）

- 删除父记录。 （在此情况下，从 `Customers` 表中删除记录。）

- 插入父记录。 （在此情况下，在 `Customers` 表中插入记录。）

- 插入子记录。 （在此情况下，在 `Orders` 表中插入记录。）

### <a name="to-delete-existing-orders"></a>删除现有顺序

- 将以下 `DeleteOrders` 方法添加到“Form1”：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet5":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet5":::

### <a name="to-delete-existing-customers"></a>删除现有客户

- 将以下 `DeleteCustomers` 方法添加到“Form1”：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet6":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet6":::

### <a name="to-add-new-customers"></a>添加新客户

- 将以下 `AddNewCustomers` 方法添加到“Form1”：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet7":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet7":::

### <a name="to-add-new-orders"></a>添加新顺序

- 将以下 `AddNewOrders` 方法添加到“Form1”：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb" id="Snippet8":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs" id="Snippet8":::

## <a name="run-the-application"></a>运行应用程序

按 **F5** 运行该应用程序。

## <a name="see-also"></a>另请参阅

- [如何：使用事务保存数据](../data-tools/save-data-by-using-a-transaction.md)
- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
