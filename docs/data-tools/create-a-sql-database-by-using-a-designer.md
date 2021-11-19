---
title: 创建数据库并添加表
description: 本教程介绍如何在数据库中使用表表设计器外键Visual Studio。 它还演示如何通过图形界面添加数据。
ms.date: 10/15/2021
ms.topic: conceptual
helpviewer_keywords:
- database tables, creating
- database files, creating
- table designer
ms.assetid: 99c2b06f-47aa-414e-8057-a3453712fd23
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 65ba75b40ca2f82422a520f6082b8a1c04f47d43
ms.sourcegitcommit: efe1d737fd660cc9183177914c18b0fd4e39ba8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2021
ms.locfileid: "130212067"
---
# <a name="create-a-database-and-add-tables-in-visual-studio"></a>在 Visual Studio 中创建一个数据库并添加表

可以使用 Visual Studio 创建和更新本地数据库SQL Server Express LocalDB。 此外，还可通过执行 SQL 工具窗口中的 Transact-SQL Server 对象资源管理器 **语句来创建** Visual Studio。 在本主题中，我们将创建 *一个 .mdf* 文件，并通过使用 表设计器。

## <a name="prerequisites"></a>先决条件

若要完成本演练，需要在 Visual Studio 中安装 **.NET** 桌面开发和数据存储和处理Visual Studio。 若要安装它们，请 **Visual Studio 安装程序，** 然后选择要修改 (版本旁边的"修改) "或"Visual Studio  >  修改"。

> [!NOTE]
> 本文中的过程仅适用于 .NET Framework Windows 窗体项目，不适用于 .NET Core Windows Forms 项目。

## <a name="create-a-project-and-a-local-database-file"></a>创建一个项目及本地数据库文件

1. 创建一个新的 **Windows 窗体应用 (.NET Framework) ，** 将其命名 **为 SampleDatabaseWalkthrough**。

2. 在菜单栏上，选择  >  **Project"添加新项"。**

3. 在项模板列表中，向下滚动并选择"基于 **服务的数据库"。**

   :::moniker range=">=vs-2022"
   ![向基于>数据库添加新项](media/vs-2022/visual-studio-add-service-database.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![向基于>数据库添加新项](media/raddata-vsitemtemplates.png)
   :::moniker-end

4. 将数据库命名 **SampleDatabase**，然后单击"添加 **"。**

### <a name="add-a-data-source"></a>添加数据源

1. 如果"**数据源"** 窗口未打开，请通过按 **Shift** Alt D 或选择菜单栏上的"查看其他数据源Windows +  +   >    >  **打开** 它。

1. 在"**数据源"窗口中**，选择 **"添加新数据源"。**

   :::moniker range=">=vs-2022"
   ![在数据源中添加Visual Studio](media/vs-2022/add-new-data-source.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![在数据源中添加Visual Studio](media/add-new-data-source.png)
   :::moniker-end

   " **数据源配置向导"随即** 打开。

1. 在"**选择数据源类型"页上**，选择"**数据库"，** 然后选择"下一 **步"。**

1. 在" **选择数据库模型"页上** ，选择 **"下一** 步"以接受默认 (数据集) 。

1. 在"**选择数据连接"页上**，选择下拉列表中的 **SampleDatabase.mdf** 文件，然后选择"下一 **步"。**

1. 在"**将连接字符串保存到应用程序配置文件**"页上，选择"下一 **步"。**

1. 在 **"选择数据库对象** "页上，会看到一条消息，指出数据库不包含任何对象。 选择“完成”。

### <a name="view-properties-of-the-data-connection"></a>查看数据连接的属性

可以通过打开数据连接属性窗口 *SampleDatabase.mdf* 文件的连接字符串：

- 选择  >  **"SQL Server 对象资源管理器"** 打开"SQL Server 对象资源管理器窗口。  展开 **(localdb) \MSSQLLocalDB** 数据库"，然后右键单击  >  *SampleDatabase.mdf* 并选择"属性 **"。**

- 或者，**如果尚未打开**  >  服务器资源管理器，可以选择"查看视图"。 展开"属性窗口连接"节点，右键单击 *SampleDatabase.mdf，* 然后选择"属性"，打开"数据连接 **"。**

  > [!TIP]
  > 如果无法展开"数据连接"节点，或者未列出 SampleDatabase.mdf **连接**，请选择连接工具栏中的"服务器资源管理器"按钮。 在"**添加连接**"**对话框中**，确保Microsoft SQL Server"数据源"下选择了"数据库文件"，然后浏览到并选择 SampleDatabase.mdf 文件。 选择"确定"，完成添加 **连接**。

## <a name="create-tables-and-keys-by-using-table-designer"></a>使用表和键创建表设计器

在本部分，你将创建两个表、每个表中的主键和几行示例数据。 还将创建一个外键，以指定一个表中的记录如何对应于另一个表中的记录。

### <a name="create-the-customers-table"></a>创建 Customers 表

1. 在 **服务器资源管理器** 中，展开" **数据连接"** 节点，然后展开 **SampleDatabase.mdf** 节点。

   如果无法展开"数据连接"节点，或者未列出 SampleDatabase.mdf **连接**，请选择连接工具栏中的"服务器资源管理器"按钮。 在"**添加连接**"**对话框中**，确保Microsoft SQL Server"数据源"下选择了"数据库文件"，然后浏览到并选择 SampleDatabase.mdf 文件。 选择"确定"，完成添加 **连接**。

2. 右键单击"表 **"，** 然后选择"**添加新表"。**

   “表设计器”将打开并显示一个网格，其中有一个默认行，表示所创建表中的一列。 通过向网格中添加行，即可在表中添加列。

3. 在网格中，为下列各个条目添加行：

   |列名称|数据类型|允许空|
   |-----------------|---------------|-----------------|
   |`CustomerID`|`nchar(5)`|False（清除）|
   |`CompanyName`|`nvarchar(50)`|False（清除）|
   |`ContactName`|`nvarchar (50)`|True（已选定）|
   |`Phone`|`nvarchar (24)`|True（已选定）|

4. 右键单击该行 `CustomerID` ，然后选择"设置 **主键"。**

5. 右键单击默认行 `Id` () ，然后选择"删除 **"。**

6. 通过更新脚本窗格的第一行来命名 Customers 表，与以下示例相匹配：

   ```sql
   CREATE TABLE [dbo].[Customers]
   ```

   你应看到与下面类似的内容：

   :::moniker range=">=vs-2022"
   ![表设计器 Customers 表](media/vs-2022/table-designer.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![表设计器 Customers 表](media/table-designer.png)
   :::moniker-end

7. 在窗口的左上角，选择 **表设计器，** 或按 **Shift**  + **Alt** + **U。**

8. 在"**预览数据库更新"** 对话框中，选择"**更新数据库"。**

   在本地数据库文件中创建 Customers 表。

### <a name="create-the-orders-table"></a>创建 Orders 表

1. 添加另一个表，然后在下表中为每个条目添加行：

   |列名称|数据类型|允许空|
   |-----------------|---------------|-----------------|
   |`OrderID`|`int`|False（清除）|
   |`CustomerID`|`nchar(5)`|False（清除）|
   |`OrderDate`|`datetime`|True（已选定）|
   |`OrderQuantity`|`int`|True（已选定）|

2. 将 **OrderID** 设置为主键，然后删除默认行。

3. 通过更新脚本窗格的第一行来命名 Orders 表，与以下示例相匹配：

   ```sql
   CREATE TABLE [dbo].[Orders]
   ```

4. 在窗口的左上角，选择 **表设计器，** 或按 **Shift**  + **Alt** + **U。**

5. 在"**预览数据库更新"** 对话框中，选择"**更新数据库"。**

   Orders 表是在本地数据库文件中创建的。 如果 **展开"表** "节点服务器资源管理器，将看到以下两个表：

   :::moniker range=">=vs-2022"
   ![表中展开的表服务器资源管理器](media/vs-2022/server-explorer-tables-node.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![表中展开的表服务器资源管理器](media/server-explorer-tables-node.png)
   :::moniker-end

   如果看不到它，点击"刷新 **工具栏"** 按钮。

### <a name="create-a-foreign-key"></a>创建外键

1. 在"订单"表表设计器网格的上下文窗格中，右键单击"外键"，然后选择"添加新 **外键"。** 

   ![在 表设计器 中添加外Visual Studio](../data-tools/media/add-foreign-key.png)

2. 在出现的文本框中，将文本 **ToTable 替换为** **Customers**。

3. 在"T-SQL"窗格中，更新最后一行以匹配以下示例：

   ```sql
   CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])
   ```

4. 在窗口的左上角，选择"表设计器"， (**Alt**   +  + **U**) 。

5. 在"**预览数据库更新"** 对话框中，选择"**更新数据库"。**

   将创建外键。

## <a name="populate-the-tables-with-data"></a>使用数据填充表

1. 在 **服务器资源管理器** 或 **SQL Server 对象资源管理器** 中，展开示例数据库的 节点。

2. 打开"表"节点的 **快捷菜单，** 选择" **刷新**"，然后展开" **表"** 节点。

3. 打开 Customers 表的快捷菜单，然后选择"**查看数据"。**

4. 为某些客户添加所需的任何数据。

    你可以指定任意五个字符作为客户 ID，但至少选择一个能记住的以便稍后在此过程中使用。

5. 打开 Orders 表的快捷菜单，然后选择"**显示表数据"。**

6. 添加某些订单的数据。 输入每一行时，该行将保存在数据库中。

    > [!IMPORTANT]
    > 确保所有订单 ID 和订单数量都是整数，并且每个客户 ID 与 Customers 表的 **CustomerID** 列中指定的值匹配。

祝贺你！ 现在，你已了解如何创建表、将其与外键链接以及添加数据。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](accessing-data-in-visual-studio.md)
