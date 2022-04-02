---
title: 创建数据库并添加表
description: 本教程介绍如何使用 Visual Studio 中的表设计器将表和外键添加到数据库。 还介绍了如何通过图形界面添加数据。
ms.date: 03/30/2022
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
ms.openlocfilehash: 40de1804c9086a201456dd2a38f0b83cc00ee006
ms.sourcegitcommit: 1ed233bb3afc5ae1f52aff8e41f7e650342033ad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2022
ms.locfileid: "141274745"
---
# <a name="create-a-database-and-add-tables-in-visual-studio"></a>在 Visual Studio 中创建一个数据库并添加表

可以使用 Visual Studio 创建和更新 SQL Server Express LocalDB 中的本地数据库文件。 还可以通过在 Visual Studio 的 SQL Server 对象资源管理器工具窗口中执行 Transact-SQL 语句来创建数据库。 在本主题中，将使用表设计器创建 .mdf 文件并添加表和键。

## <a name="prerequisites"></a>先决条件

要完成本演练，将需要在 Visual Studio 中安装 .NET 桌面部署以及“数据存储和处理”工作负载。 若要安装这些程序，请打开 Visual Studio 安装程序，然后在要修改的 Visual Studio 版本旁选择“修改”（或“更多” > “修改”）。

> [!NOTE]
> 本文中的步骤仅适用于 .NET Framework Windows 窗体项目，不适用于 .NET Core Windows 窗体项目。

## <a name="create-a-project-and-a-local-database-file"></a>创建一个项目及本地数据库文件

1. 创建一个新的 Windows 窗体应用 (.NET Framework) 项目，并将其命名为 SampleDatabaseWalkthrough。

2. 在菜单栏上，依次选择“项目” > “添加新项”。

3. 在项模板列表中，向下滚动并选择“基于服务的数据库”。

   :::moniker range=">=vs-2022"
   ![“添加新项”>“基于服务的数据库”](media/vs-2022/visual-studio-add-service-database.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![“添加新项”>“基于服务的数据库”](media/raddata-vsitemtemplates.png)
   :::moniker-end

4. 将数据库命名为 SampleDatabase，然后单击“添加”。

### <a name="add-a-data-source"></a>添加数据源

1. 如果“数据源”窗口未打开，通过按 Shift + Alt + D 或选择菜单栏上的“查看” > “其他窗口”“数据源” > 来将其打开。

1. 在“数据源”窗口中，选择“添加新的数据源”。

   :::moniker range=">=vs-2022"
   ![在 Visual Studio 中添加新数据源](media/vs-2022/add-new-data-source.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![在 Visual Studio 中添加新数据源](media/add-new-data-source.png)
   :::moniker-end

   “数据源配置”向导随即打开。

1. 在“选择数据源类型”页上，选择“数据库”，然后单击“下一步”。

1. 在“选择数据库模型”页上，选择“下一步”以接受默认（数据集）。

1. 在“选择数据连接”页上，在下拉列表中选择 SampleDatabase.mdf 文件，然后选择“下一步”。

1. 在“将连接字符串保存到应用程序配置文件”页上，选择“下一步”。

1. 在“选择数据库对象”页上，将看到提示数据库不包含任何对象的消息。 选择“完成”。

### <a name="view-properties-of-the-data-connection"></a>查看数据连接的属性

可以通过打开数据连接的“属性”窗口来查看 SampleDatabase.mdf 文件的连接字符串：

- 选择“查看” > “SQL Server 对象资源管理器”以打开“SQL Server 对象资源管理器”窗口。 展开“(localdb)\MSSQLLocalDB” > “数据库”，然后右键单击 SampleDatabase.mdf 并选择“属性”。

- 或者，如果窗口尚未打开，则可以选择“查看” > “服务器资源管理器”。 通过展开“数据连接”节点、右键单击 SampleDatabase.mdf，然后选择“属性”可以打开“属性”窗口。

  > [!TIP]
  > 如果无法展开“数据连接”接口或未列出 SampleDatabase.mdf 连接，请选择“服务器资源管理器”工具栏中的“连接到数据库”按钮。 在“添加连接”对话框中，确保在“数据源”下选择了“Microsoft SQL Server 数据库文件”，然后浏览到 SampleDatabase.mdf 文件并选择该文件。  通过选择“确定”完成添加连接。

## <a name="create-tables-and-keys-by-using-table-designer"></a>使用表设计器创建表和键

在本节中，你将创建两个表，每个表中有一个主键和几行示例数据。 你还将创建外键以指定一个表中的记录如何对应于另一个表中的记录。

### <a name="create-the-customers-table"></a>创建 Customers 表

1. 在“服务器资源管理器”中，依次展开“数据连接”节点和“SampleDatabase.mdf”节点。  

   如果无法展开“数据连接”接口或未列出 SampleDatabase.mdf 连接，请选择“服务器资源管理器”工具栏中的“连接到数据库”按钮。 在“添加连接”对话框中，确保在“数据源”下选择了“Microsoft SQL Server 数据库文件”，然后浏览到 SampleDatabase.mdf 文件并选择该文件。  通过选择“确定”完成添加连接。

2. 右键单击“表”，然后选择“添加新表” 。

   “表设计器”将打开并显示一个网格，其中有一个默认行，表示所创建表中的一列。 通过向网格中添加行，即可在表中添加列。

3. 在网格中，为下列各个条目添加行：

   |列名称|数据类型|允许空|
   |-----------------|---------------|-----------------|
   |`CustomerID`|`nchar(5)`|False（清除）|
   |`CompanyName`|`nvarchar(50)`|False（清除）|
   |`ContactName`|`nvarchar (50)`|True（已选定）|
   |`Phone`|`nvarchar (24)`|True（已选定）|

4. 在 `CustomerID` 行上右键单击，然后选择“设置主键”。

5. 在默认行 (`Id`) 上右键单击，然后选择“删除”。

6. 通过更新脚本窗格的第一行来命名 Customers 表，与以下示例相匹配：

   ```sql
   CREATE TABLE [dbo].[Customers]
   ```

7. 将索引约束添加到 Customers 表。 在行的末尾 `Phone` 添加一个逗号，然后在右括号前面添加以下示例：

   ```sql
   CONSTRAINT [PK_Customers] PRIMARY KEY ([CustomerID])
   ```

   你应看到与下面类似的内容：

   :::moniker range=">=vs-2022"
   ![具有 Customers 表的表设计器](media/vs-2022/table-designer.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![具有 Customers 表的表设计器](media/table-designer.png)
   :::moniker-end

8. 在“表设计器”的左上角中，选择“更新”，或按 Shift + Alt + U。

9. 在“预览数据库更新”对话框中，选择“更新数据库”。

   在本地数据库文件中创建了 Customers 表。

### <a name="create-the-orders-table"></a>创建 Orders 表

1. 添加另一个表，然后在下表中为每个条目添加行：

   |列名称|数据类型|允许空|
   |-----------------|---------------|-----------------|
   |`OrderID`|`int`|False（清除）|
   |`CustomerID`|`nchar(5)`|False（清除）|
   |`OrderDate`|`datetime`|True（已选定）|
   |`OrderQuantity`|`int`|True（已选定）|

2. 将“OrderID”设置为主键，然后删除默认行。

3. 通过更新脚本窗格的第一行来命名 Orders 表，与以下示例相匹配：

   ```sql
   CREATE TABLE [dbo].[Orders]
   ```

4. 将索引约束添加到 Customers 表。 在行的末尾 `OrderQuantity` 添加一个逗号，然后在右括号前面添加以下示例：

   ```sql
   CONSTRAINT [PK_Orders] PRIMARY KEY ([OrderId])
   ```

5. 在“表设计器”的左上角中，选择“更新”，或按 Shift + Alt + U。

6. 在“预览数据库更新”对话框中，选择“更新数据库”。

   在本地数据库文件中创建了 Orders 表。 如果在服务器资源管理器中展开“表”节点，则可以看到两个表：

   :::moniker range=">=vs-2022"
   ![服务器资源管理器中展开的“表”节点](media/vs-2022/server-explorer-tables-node.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![服务器资源管理器中展开的“表”节点](media/server-explorer-tables-node.png)
   :::moniker-end

   如果看不到，则点击“刷新”工具栏按钮。

### <a name="create-a-foreign-key"></a>创建外键

1. 在 Orders 表的“表设计器”网格的右侧上下文窗格中，右键单击“外键”，然后选择“添加新的外键”。 

   :::moniker range=">=vs-2022"
   ![在 Visual Studio 的表设计器中添加外键](media/vs-2022/add-foreign-key.png)
   :::moniker-end
   :::moniker range="<=vs-2019"
   ![在 Visual Studio 的表设计器中添加外键](../data-tools/media/add-foreign-key.png)
   :::moniker-end

2. 在显示的文本框中，将文本“ToTable”替换为“Customers” 。

3. 在 T-SQL 窗格中，更新最后一行以与以下示例相匹配：

   ```sql
   CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])
   ```

4. 在“表设计器”的左上角中，选择“更新”(Shift + Alt + U)。

5. 在“预览数据库更新”对话框中，选择“更新数据库”。

   将创建外键。

## <a name="populate-the-tables-with-data"></a>将数据填入表中

1. 在“服务器资源管理器”或“SQL Server 对象资源管理器”中，展开示例数据库的节点。 

2. 打开“表”节点的快捷菜单，选择“刷新”，然后展开“表”节点。  

3. 打开 "Customers" 表的快捷菜单，然后选择 " **显示表数据** " 或 " **查看数据**"。

4. 为一些客户添加任何所需数据。

    你可以指定任意五个字符作为客户 ID，但至少选择一个能记住的以便稍后在此过程中使用。

5. 打开 Orders 表的快捷菜单，然后选择 " **显示表数据** " 或 " **查看数据**"。

6. 为一些订单添加数据。 输入每一行时，该行将保存在数据库中。

    > [!IMPORTANT]
    > 请确保所有订单 ID 和订单数量是整数，并且每个客户 ID 与 Customers 表中的“CustomerID”列中指定的值匹配。

祝贺你！ 现在已经了解如何创建表、将其与外键链接并添加数据。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](accessing-data-in-visual-studio.md)
