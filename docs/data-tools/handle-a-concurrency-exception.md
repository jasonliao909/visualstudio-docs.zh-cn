---
title: 处理并发异常
description: 处理并发异常 (System.data.dbconcurrencyexception) ，当两个用户尝试同时更改数据库中的相同数据时，将引发此异常。
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
ms.openlocfilehash: 6195fa7e27c6c6f72166dfc00ba888f3644cfe23cb6b38570f4ba6502f458054
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121347176"
---
# <a name="handle-a-concurrency-exception"></a>处理并发异常

<xref:System.Data.DBConcurrencyException?displayProperty=fullName>当两个用户尝试同时更改数据库中的相同数据时，将引发并发异常 () 。 在本演练中，你将创建一个 Windows 应用程序，该应用程序演示如何捕获 <xref:System.Data.DBConcurrencyException> 、找到导致错误的行，并了解如何处理该错误的策略。

本演练将引导你完成以下过程：

1. 创建新的 **Windows 窗体应用程序** 项目。

2. 基于 Northwind Customers 表创建新的数据集。

3. 使用创建窗体 <xref:System.Windows.Forms.DataGridView> 以显示数据。

4. 使用 Northwind 数据库的 Customers 表中的数据填充数据集。

5. 使用 **服务器资源管理器** 中的 "**显示表数据**" 功能可访问客户表的数据和更改记录。

6. 将相同的记录更改为其他值，更新数据集，并尝试将更改写入数据库，这将导致引发并发错误。

7. 捕获错误，然后显示记录的不同版本，使用户能够确定是继续更新数据库，还是取消更新。

## <a name="prerequisites"></a>必备条件

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果没有 LocalDB SQL Server Express，请从 [SQL Server Express 下载页面](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过 **Visual Studio 安装程序** 安装。 在 **Visual Studio 安装程序** 中，你可以将 SQL Server Express LocalDB 作为 **数据存储和处理** 工作负荷的一部分进行安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开 **SQL Server 对象资源管理器**"窗口。  (SQL Server 对象资源管理器作为 Visual Studio 安装程序中的 **数据存储和处理** 工作负荷的一部分安装。 ) 展开 **SQL Server** 节点。 右键单击 LocalDB 实例，然后选择 "**新建查询**"。

       此时将打开查询编辑器窗口。

    2. 将[Northwind transact-sql SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 t-sql SQL 脚本从头开始创建 Northwind 数据库，并用数据填充它。

    3. 将 SQL 脚本粘贴到查询编辑器中，然后选择 "**执行**" 按钮。

       一小段时间后，查询将完成运行，并创建 Northwind 数据库。

## <a name="create-a-new-project"></a>创建新项目

首先创建一个新的 Windows 窗体应用程序：

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”    。

2. 在左侧窗格中展开 " **Visual c #** " 或 " **Visual Basic** "，然后选择 " **Windows 桌面**"。

3. 在中间窗格中，选择 " **Windows 窗体应用程序**" 项目类型。

4. 将项目命名为 **ConcurrencyWalkthrough**，然后选择 **"确定"**。

     将创建 **ConcurrencyWalkthrough** 项目并将其添加到 **解决方案资源管理器**，并在设计器中打开新窗体。

## <a name="create-the-northwind-dataset"></a>创建 Northwind 数据集

接下来，创建一个名为 **NorthwindDataSet** 的数据集：

1. 在 " **数据** " 菜单上，选择 " **添加新数据源**"。

   “数据源配置”向导随即打开。

2. 在 " **选择数据源类型** " 屏幕上，选择 " **数据库**"。

   ![Visual Studio 中的数据源配置向导](media/data-source-configuration-wizard.png)

3. 从可用连接的列表中选择与 Northwind 示例数据库的连接。 如果连接列表中的连接不可用，请选择 " **新建连接**"。

    > [!NOTE]
    > 如果要连接到本地数据库文件，请在询问是否要将文件添加到项目时，选择 " **否** "。

4. 在 "将 **连接字符串保存到应用程序配置文件** " 屏幕上，选择 " **下一步**"。

5. 展开 " **表** " 节点，然后选择 " **Customers** " 表。 数据集的默认名称应为 **NorthwindDataSet**。

6. 选择 " **完成** " 将数据集添加到项目。

## <a name="create-a-data-bound-datagridview-control"></a>创建数据绑定 DataGridView 控件

在本部分中，将 <xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType> 通过将 "**客户**" 项从 "**数据源**" 窗口拖动到 Windows 窗体来创建。

1. 若要打开 " **数据源** " 窗口，请在 " **数据** " 菜单上，选择 " **显示数据源**"。

2. 在 " **数据源** " 窗口中，展开 " **NorthwindDataSet** " 节点，然后选择 " **Customers** " 表。

3. 选择 "表" 节点上的向下箭头，然后在下拉列表中选择 " **DataGridView** "。

4. 将该表拖到窗体的空白区域。

     <xref:System.Windows.Forms.DataGridView>名为 **CustomersDataGridView** 的控件和一个 <xref:System.Windows.Forms.BindingNavigator> 名为 **CustomersBindingNavigator** 的控件将添加到绑定到的窗体中 <xref:System.Windows.Forms.BindingSource> 。 这反过来又绑定到 NorthwindDataSet 中的 Customers 表。

## <a name="test-the-form"></a>测试窗体

你现在可以测试窗体，确保它在此点之前的行为正常：

1. 选择 **F5** 以运行应用程序。

     窗体上将显示一个 <xref:System.Windows.Forms.DataGridView> 控件，其中填充了 "Customers" 表中的数据。

2. 在“调试”菜单中，选择“停止调试”。

## <a name="handle-concurrency-errors"></a>处理并发错误

处理错误的方式取决于控制应用程序的特定业务规则。 对于本演练，我们将使用以下策略作为如何处理并发错误的示例。

该应用程序为用户提供了记录的三个版本：

- 数据库中的当前记录

- 加载到数据集中的原始记录

- 数据集中的建议更改

然后，用户可以用建议的版本覆盖数据库，或取消更新，并通过数据库中的新值刷新数据集。

### <a name="to-enable-the-handling-of-concurrency-errors"></a>启用并发错误处理

1. 创建自定义错误处理程序。

2. 向用户显示选择。

3. 处理用户的响应。

4. 重新发送更新，或重置数据集中的数据。

### <a name="add-code-to-handle-the-concurrency-exception"></a>添加代码以处理并发异常

当你尝试执行更新并引发异常时，通常需要使用引发的异常提供的信息来执行某些操作。 在本部分中，将添加尝试更新数据库的代码。 还处理 <xref:System.Data.DBConcurrencyException> 可能引发的任何，以及任何其他异常。

> [!NOTE]
> `CreateMessage` `ProcessDialogResults` 稍后将在本演练中添加和方法。

1. 在方法下面添加以下代码 `Form1_Load` ：

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet1":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet1":::

2. 替换 `CustomersBindingNavigatorSaveItem_Click` 方法以调用方法，如下所示 `UpdateDatabase` ：

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet2":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet2":::

### <a name="display-choices-to-the-user"></a>向用户显示选项

刚编写的代码调用 `CreateMessage` 过程向用户显示错误信息。 对于本演练，您将使用消息框向用户显示该记录的不同版本。 这样，用户就可以选择是用更改覆盖记录还是取消编辑。 一旦用户选择某个选项 (单击消息框上的按钮) ，就会将响应传递到该 `ProcessDialogResult` 方法。

通过将以下代码添加到 **代码编辑器** 来创建消息。 在方法下面输入以下代码 `UpdateDatabase` ：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet4":::

### <a name="process-the-users-response"></a>处理用户的响应

还需要代码来处理用户对消息框的响应。 这些选项可以用建议的更改覆盖数据库中的当前记录，也可以放弃本地更改并刷新包含数据库中当前记录的数据表。 如果用户选择 **"是"**，则 <xref:System.Data.DataTable.Merge%2A> 会调用方法，并将 *preserveChanges* 参数设置为 **true**。 这会导致更新尝试成功，因为原始版本的记录现在与数据库中的记录匹配。

在上一部分中添加的代码下面添加以下代码：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConcurrency/CS/Form1.cs" id="Snippet3":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConcurrency/VB/Form1.vb" id="Snippet3":::

## <a name="test-the-form-behavior"></a>测试窗体行为

你现在可以对窗体进行测试，以确保它按预期方式运行。 若要模拟并发冲突，请在填写 NorthwindDataSet 后更改数据库中的数据。

1. 选择 **F5** 以运行应用程序。

2. 窗体显示后，使其保持运行状态，并切换到 Visual Studio IDE。

3. 在“视图”菜单中，选择“服务器资源管理器”。

4. 在 **服务器资源管理器** 中，展开应用程序正在使用的连接，然后展开 " **表** " 节点。

5. 右键单击 **Customers** 表，然后选择 " **显示表数据**"。

6. 在第一条记录 (**ALFKI**) 中，将 " **联系人姓名** " 改为 " **Maria Anders2**"。

    > [!NOTE]
    > 导航到不同的行以提交更改。

7. 切换到 ConcurrencyWalkthrough 的运行形式。

8. 在表单 (**ALFKI**) 的第一条记录中，将 " **联系人姓名** " 改为 " **Maria Anders1**"。

9. 选择“保存”按钮。

     引发并发错误，并显示消息框。

   选择 " **否** " 将取消更新并用数据库中当前的值更新数据集。 选择 **"是"** 将建议的值写入数据库。

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
