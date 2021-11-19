---
title: 处理并发异常
description: 处理并发异常 (System.Data.DBConcurrencyException)，当两个用户同时尝试更改数据库中的相同数据时，将引发此异常。
ms.custom: SEO-VS-2020
ms.date: 09/11/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: ac64e951c5307d0fe940e6ec92c2e35a727e3811
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601151"
---
# <a name="handle-a-concurrency-exception"></a>处理并发异常

在当两个用户同时尝试更改数据库中的相同数据时，将引发并发异常 (<xref:System.Data.DBConcurrencyException?displayProperty=fullName>)。 本演练将创建一个 Windows 应用程序，该应用程序演示如何捕获 <xref:System.Data.DBConcurrencyException>，找导致错误的行，并了解处理该错误的策略。

本演练将指导你完成以下过程：

1. 创建新的 **Windows 窗体应用程序** 项目。

2. 基于 Northwind Customers 表创建新的数据集。

3. 使用 <xref:System.Windows.Forms.DataGridView> 创建窗体以显示数据。

4. 使用 Northwind 数据库中的 Customers 表中的数据填充数据集。

5. 使用服务器资源管理器中的“显示表数据”功能，访问 Customers 表的数据并更改一条记录。 

6. 将同一记录更改为其他值，更新数据集，并尝试将更改写入数据库，这导致引发并发错误。

7. 捕获该错误，然后显示该记录的不同版本，允许用户确定是继续更新数据库还是取消更新。

## <a name="prerequisites"></a>先决条件

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果尚未安装 SQL Server Express LocalDB，可以从 [SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过 Visual Studio 安装程序安装。 在 Visual Studio 安装程序中，可以将 SQL Server Express LocalDB 作为数据存储和处理工作负载的一部分或作为单个组件进行安装 。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开“SQL Server 对象资源管理器”窗口。 （在 Visual Studio 安装程序中 SQL Server 对象资源管理器作为数据存储和处理工作负载的一部分安装。）展开 SQL Server 节点 。 右键单击 LocalDB 实例并选择“新建查询”。

       此时将打开查询编辑器窗口。

    2. 将 [Northwind Transact-SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-SQL 脚本从头开始创建 Northwind 数据库并用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器中，然后选择“执行”按钮。

       不久后，查询完成运行并且 Northwind 数据库创建完成。

## <a name="create-a-new-project"></a>创建新项目

从创建新的 Windows 窗体应用程序开始：

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 在左侧窗格中展开“Visual C#”或“Visual Basic”，然后选择“Windows 桌面”  。

3. 在中间窗格中，选择“Windows 窗体应用”项目类型。

4. 将项目命名为“ConcurrencyWalkthrough”，然后选择“确定” 。

     将创建 ConcurrencyWalkthrough 项目并将其添加到解决方案资源管理器，并在设计器中打开新窗体。 

## <a name="create-the-northwind-dataset"></a>创建 Northwind 数据集

接下来，创建一个名为 NorthwindDataSet 的数据集：

1. 在“数据”菜单上，选择“添加新数据源”。 

   “数据源配置”向导随即打开。

2. 在“选择数据源类型”屏幕上，选择“数据库”。 

   ![Visual Studio 中的数据源配置向导](media/data-source-configuration-wizard.png)

3. 从可用连接列表中选择与 Northwind 示例数据库的连接。 如果该连接不在连接列表中，请选择“新建连接”。

    > [!NOTE]
    > 如果要连接到本地数据库文件，请在系统询问是否将文件添加到项目时选择“否”。

4. 在“将连接字符串保存到应用程序配置文件”屏幕中，选择“下一步” 。

5. 展开“Tables”节点，然后选择“Customers”表。  数据集的默认名称应为 NorthwindDataSet。

6. 选择“完成”，将数据集添加到项目。

## <a name="create-a-data-bound-datagridview-control"></a>创建数据绑定 DataGridView 控件

在本部分中，你要将“Customers”项通过从“数据源”窗口拖动到 Windows 窗体来创建 <xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType> 。

1. 若要打开“数据源”窗口，在“数据”菜单上选择“显示数据源”  。

2. 在“数据源”窗口中，展开“NorthwindDataSet”节点，然后选择“Customers”表。  

3. 选择表节点上的向下箭头，然后在下拉列表中选择“DataGridView”。

4. 将表拖到窗体上的空白区域。

     名为 CustomersDataGridView 的 <xref:System.Windows.Forms.DataGridView> 控件和名为 CustomersBindingNavigator 的 <xref:System.Windows.Forms.BindingNavigator> 控件将添加到绑定到 <xref:System.Windows.Forms.BindingSource> 的窗体中。 而这又绑定到 NorthwindDataSet 中的 Customers 表。

## <a name="test-the-form"></a>测试窗体

现在可以测试窗体，以确保它的行为迄今为止符合预期：

1. 选择 F5 运行该应用程序。

     将会显示窗体，其中有一个 <xref:System.Windows.Forms.DataGridView> 控件，该控件用 Customers 表中的数据填充。

2. 在“调试”菜单中，选择“停止调试”。

## <a name="handle-concurrency-errors"></a>处理并发错误

如何处理错误取决于用于管控应用程序的特定业务规则。 对于本演练，我们将使用以下策略作为如何处理并发错误的示例。

应用程序向用户显示记录的三个版本：

- 数据库中的当前记录

- 加载到数据集中的原始记录

- 数据集中建议的更改

然后，用户可以使用建议的版本覆盖数据库，或者取消更新，然后使用数据库中的新值刷新数据集。

### <a name="to-enable-the-handling-of-concurrency-errors"></a>若要启用并发错误处理

1. 创建自定义错误处理程序。

2. 向用户显示选项。

3. 处理用户的响应。

4. 重新发送更新，或重置数据集中的数据。

### <a name="add-code-to-handle-the-concurrency-exception"></a>添加代码以处理并发异常

尝试执行更新并引发异常时，通常需要利用所引发异常提供的信息执行某些操作。 在本部分，你将添加尝试更新数据库的代码。 还要处理可能会引发的任何 <xref:System.Data.DBConcurrencyException> 以及任何其他异常。

> [!NOTE]
> 稍后将在本演练中添加 `CreateMessage` 和 `ProcessDialogResults` 方法。

1. 在 `Form1_Load` 方法下面添加以下代码：

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet1":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet1":::

2. 替换 `CustomersBindingNavigatorSaveItem_Click` 方法，使其调用 `UpdateDatabase` 方法，如下所示：

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet2":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet2":::

### <a name="display-choices-to-the-user"></a>向用户显示选项

刚编写的代码调用 `CreateMessage` 过程，以向用户显示错误信息。 对于本演练，你将使用消息框向用户显示记录的不同版本。 这使用户可以选择是使用更改覆盖记录还是取消编辑。 用户在消息框上选择选项（单击按钮）后，响应将传递给 `ProcessDialogResult` 方法。

通过将以下代码添加到代码编辑器来创建消息。 在 `UpdateDatabase` 方法下输入以下代码：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet4":::

### <a name="process-the-users-response"></a>处理用户的响应

还需要代码来处理用户对消息框的响应。 可以选择使用建议的更改覆盖数据库中的当前记录，或者放弃本地更改，然后使用数据库中当前的记录刷新数据表。 如果用户选择“是”，将调用 <xref:System.Data.DataTable.Merge%2A> 方法，同时将 preserveChanges 参数设置为 true。 这会使得更新尝试成功，因为记录的原始版本现在与数据库中的记录匹配。

在上一部分中添加的代码下方添加以下代码：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet3":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet3":::

## <a name="test-the-form-behavior"></a>测试窗体行为

现在可以测试窗体，以确保它的行为符合预期。 若要模拟并发冲突，请在填充 NorthwindDataSet 后更改数据库中的数据。

1. 选择 F5 运行该应用程序。

2. 窗体出现后，让窗体保持运行状态并切换到 Visual Studio IDE。

3. 在“视图”菜单中，选择“服务器资源管理器”。

4. 在服务器资源管理器中，展开你的应用程序使用的连接，然后展开“Tables”节点 。

5. 右键单击“Customers”表，然后选择“显示表数据”。 

6. 在第一条记录 (ALFKI) 中，将 ContactName 改为“Maria Anders2”。  

    > [!NOTE]
    > 导航到其他行以提交更改。

7. 切换到 ConcurrencyWalkthrough 的运行窗体。

8. 在表单上的第一条记录 (ALFKI) 中，将 ContactName 改为“Maria Anders1”。  

9. 选择“保存”按钮。

     将引发并发错误，并显示消息框。

   选择“否”将取消更新并用数据库中当前的值更新数据集。 选择“是”会将建议的值写入数据库。

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
