---
title: 将数据保存到数据库（多个表）
description: 在本演练中，使用 Visual Studio 中的数据集工具将多个表中的数据保存到数据库。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: cc0af4b3a6905e472a2d5cc4b3340adad5199fe1
ms.sourcegitcommit: 7a300823cf1bd3355be03bde561cf2777bc09eae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2021
ms.locfileid: "133977661"
---
# <a name="save-data-to-a-database-multiple-tables"></a>将数据保存到数据库（多个表）

应用程序开发中最常用方案之一是在 Windows 应用程序窗体上显示数据、编辑数据并将更新后的数据发回数据库。 本演练创建可显示两个相关表的数据的窗体，并显示如何编辑记录和将更改保存回数据库。 此示例使用源自 Northwind 示例数据库的 `Customers` 和 `Orders` 表。

通过调用 TableAdapter 的 `Update` 方法，可以将应用程序中的数据保存回数据库。 将表从“数据源”窗口拖动到窗体上时，将自动添加保存数据所需的代码。 添加到窗体中的任何其他表都要求手动添加此代码。 本演练显示了如何添加从多个表保存更新的代码。

本演练涉及以下任务：

- 使用[数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)在应用程序中创建和配置数据源。

- 在[数据源窗口](add-new-data-sources.md#data-sources-window)中设置项的控件。 有关详细信息，请参阅[设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

- 通过将某些项从“数据源”窗口拖动到窗体上来创建数据绑定控件。

- 修改数据集的每个表中的一些记录。

- 修改用于将数据集中的更新后的数据发回数据库的代码。

## <a name="prerequisites"></a>先决条件

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果尚未安装 SQL Server Express LocalDB，可以从 [SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过 Visual Studio 安装程序安装。 在 Visual Studio 安装程序中，可以将 SQL Server Express LocalDB 作为数据存储和处理工作负载的一部分或作为单个组件进行安装 。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开“SQL Server 对象资源管理器”窗口。 （在 Visual Studio 安装程序中 SQL Server 对象资源管理器作为数据存储和处理工作负载的一部分安装。）展开 SQL Server 节点 。 右键单击 LocalDB 实例并选择“新建查询”。

       此时将打开查询编辑器窗口。

    2. 将 [Northwind Transact-SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/main/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL 脚本从头开始创建 Northwind 数据库并用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器中，然后选择“执行”按钮。

       不久后，查询完成运行并且 Northwind 数据库创建完成。

## <a name="create-the-windows-forms-application"></a>创建 Windows 窗体应用程序

为 C# 或 Visual Basic 创建一个新的 Windows 窗体应用项目。 将项目命名为 **UpdateMultipleTablesWalkthrough**。

## <a name="create-the-data-source"></a>创建数据源

此步骤使用“数据源配置向导”从 Northwind 数据库创建一个数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅[如何：安装示例数据库](../data-tools/installing-database-systems-tools-and-samples.md)。

1. 在“数据”菜单上，选择“显示数据源” 。

   “数据源”窗口随即打开。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 在“选择数据源类型”屏幕中，选择“数据库”，然后选择“下一步”  。

4. 在“选择数据连接”屏幕中，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

         -或-

    - 选择“新建连接”，打开“添加/修改连接”对话框。

5. 如果数据库需要密码，请选择包含敏感数据的选项，再选择“下一步”。

6. 在“将连接字符串保存到应用程序配置文件”中，选择“下一步” 。

7. 在“选择数据库对象”屏幕中，展开“表”节点 。

8. 选择“Customers”和“Orders”表，然后选择“完成”  。

     “NorthwindDataSet”将添加到项目，这些表将显示在“数据源”窗口中。

## <a name="set-the-controls-to-be-created"></a>设置要创建的控件

对于本演练，`Customers` 表中数据将采用“详细信息”布局（数据在单独控件中显示）。 `Orders` 表中的数据将采用“网格”布局（在 <xref:System.Windows.Forms.DataGridView> 控件中显示）。

### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>设置“数据源”窗口中项的拖放类型

1. 在“数据源”窗口中展开“客户”节点 。

2. 在“客户”节点上，选择控件列表中的“详细信息”，将“客户”表的控件更改为单个控件  。 有关详细信息，请参阅[设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

## <a name="create-the-data-bound-form"></a>创建数据绑定窗体

通过将某些项从“数据源”窗口拖到窗体，可创建数据绑定控件。

1. 将主“Customers”节点从“数据源”窗口拖到“Form1”上。

     带有描述性标签的数据绑定控件将显示在窗体上，同时还显示一个工具条 (<xref:System.Windows.Forms.BindingNavigator>)，用于在记录间进行导航。 此时组件栏中显示 [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、`CustomersTableAdapter`、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

2. 将相关的“Orders”节点从“数据源”窗口拖到“Form1”上。

    > [!NOTE]
    > 相关的“Orders”节点位于“Fax”列下，该节点是“Customers”节点的子节点。

     用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 组件栏中显示 `OrdersTableAdapter` 和 <xref:System.Windows.Forms.BindingSource>。

## <a name="add-code-to-update-the-database"></a>添加用于更新数据库的代码

通过调用“Customers”和“Orders”TableAdapter 的 `Update` 方法，可更新数据库。 默认情况下，<xref:System.Windows.Forms.BindingNavigator> 的“保存”按钮的事件处理程序将添加到窗体代码中，以将更新内容发送到数据库。 本过程将修改该代码以按正确的顺序发送更新内容。这将消除产生引用完整性错误的可能性。 该代码还将通过在 try-catch 块中包装更新调用来实现错误处理。 可以根据应用程序的需要修改代码。

> [!NOTE]
> 为清楚起见，本演练不使用事务。 但是，如果要更新两个或多个相关表，请在事务中包含所有更新逻辑。 事务是指一个过程，它确保在提交更改之前对数据库的所有相关更改均可成功完成。 有关详细信息，请参阅[事务和并发](/dotnet/framework/data/adonet/transactions-and-concurrency)。

### <a name="to-add-update-logic-to-the-application"></a>将更新逻辑添加到应用程序

1. 选择 <xref:System.Windows.Forms.BindingNavigator> 上的“保存”按钮。 这会将代码编辑器打开到 `bindingNavigatorSaveItem_Click` 事件处理程序。

2. 替换事件处理程序中的代码以调用相关 TableAdapter 的 `Update` 方法。 下面的代码首先创建三个临时数据表以保存每个 <xref:System.Data.DataRowState> 的更新信息（<xref:System.Data.DataRowState.Deleted>、<xref:System.Data.DataRowState.Added> 和 <xref:System.Data.DataRowState.Modified>）。 更新按正确的顺序运行。 代码应类似于：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form4.vb" id="Snippet10":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form4.cs" id="Snippet10":::

## <a name="test-the-application"></a>测试应用程序

1. 按 **F5**。

2. 对每个表中的一条或多条记录的数据执行一些更改。

3. 选择“保存”按钮。

4. 检查数据库中的值以验证更改是否已保存。

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
