---
title: 创建和配置 TableAdapter
description: 查看如何在 Visual Studio 中创建和配置 TableAdapter。 TableAdapters 提供应用程序和数据库之间的通信。
ms.custom: SEO-VS-2020
ms.date: 09/01/2017
ms.topic: how-to
helpviewer_keywords:
- table adapters, creating
- creating TableAdapters
- data [Visual Studio], creating data components
- data [Visual Studio], TableAdapters
- data [Visual Studio], creating table adapters
ms.assetid: 08630d69-0d6c-4e8f-b42d-2922f45f8415
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 024511b6bec5d060018c2a4976b17d22357ccaa8789a716af14debb037e91169
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121347464"
---
# <a name="create-and-configure-tableadapters"></a>创建和配置 TableAdapter

TableAdapters 提供应用程序和数据库之间的通信。 它们连接到数据库、运行查询或存储过程，并返回新的数据表，或者使用返回的数据填充 <xref:System.Data.DataTable> 现有数据。 TableAdapters 还可以将更新后的数据从应用程序发送回数据库。

执行下列操作之一时，将创建 TableAdapters：

- 将数据库对象从 **服务器资源管理器****拖动到** 数据集设计器 中。

- 运行数据源配置向导，并选择"数据库 **"或****"Web 服务**"数据源类型。

   ![数据源配置向导Visual Studio](media/data-source-configuration-wizard.png)

还可以创建新的 TableAdapter，然后使用数据源对其进行配置，只需将 TableAdapter 从"工具箱"拖动到表图面上的 **数据集设计器区域即可**。

有关 TableAdapters 的简介，请参阅 [使用 TableAdapters 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="use-the-tableadapter-configuration-wizard"></a>使用 TableAdapter 配置向导

运行 **TableAdapter 配置向导** 以创建或编辑 TableAdapter 及其关联的 DataTable。 可以通过右键单击现有 TableAdapter，在 **数据集设计器。**

![raddata 表适配器配置向导](../data-tools/media/raddata-table-adapter-configuration-wizard.png)

如果在焦点位于"工具箱"中拖动新的 TableAdapter数据集设计器向导将启动并提示你指定 TableAdapter 应连接到的数据源。 下一页中，向导将询问它应该使用哪种命令来与数据库通信，SQL语句或存储过程。  (如果配置已与数据源关联的 TableAdapter，则看不到) 

- 如果具有数据库的正确权限，可以选择在基础数据库中创建新的存储过程。 如果没有这些权限，则不能这样做。

- 还可以选择为 TableAdapter 的SELECT、INSERT、UPDATE和 **DELETE** 命令运行现有存储过程。  例如，分配给 **Update** 命令存储过程在调用 方法时 `TableAdapter.Update()` 运行。

将参数从选中的存储过程映射到数据表中相应的列。 例如，如果存储过程接受一个名为 的参数，该参数传递给表中的列，则将 参数的 `@CompanyName` `CompanyName` **源** 列 `@CompanyName` 设置为 `CompanyName` 。

> [!NOTE]
> 通过调用在向导下一步中命名的 TableAdapter 的 方法来运行分配给 SELECT 命令存储过程。 默认方法是 `Fill` ，因此通常用于运行 SELECT 过程的代码为 `TableAdapter.Fill(tableName)` 。 如果从 更改默认名称，请将 替换为分配的名称，并将 `Fill` `Fill` "TableAdapter"替换为 TableAdapter (例如 `CustomersTableAdapter`) 。

- 选择 **"创建方法以将更新直接发送到数据库"** 选项等效于将 `GenerateDBDirectMethods` 属性设置为 true。 当原始 SQL 语句未提供足够的信息或查询不是可更新的查询时，此选项不可用。 例如，在 **JOIN** 查询和返回单个标量值 (查询) 这种情况。

向导 **中的** "高级选项"使你可以：

- 基于在"生成语句"页上定义的 SELECT 语句生成 INSERT、UPDATE **SQL DELETE** 语句
- 使用开放式并发
- 指定是否在运行 INSERT 和 UPDATE 语句后刷新数据表

## <a name="configure-a-tableadapters-fill-method"></a>配置 TableAdapter 的 Fill 方法

有时，你可能想要更改 TableAdapter 表的架构。 为此，请修改 TableAdapter 的主 `Fill` 方法。 使用定义关联数据表架构的主方法创建 `Fill` TableAdapters。 主要 `Fill` 方法基于最初配置 TableAdapter 时输入的查询或存储过程。 它是数据集设计器 (数据) 下的最顶层方法。

![带有多个查询的 TableAdapter](../data-tools/media/tableadapter.gif)

对 TableAdapter 的 main 方法进行的任何 `Fill` 更改都反映在关联数据表的架构中。 例如，从 main 方法中的查询中删除列 `Fill` 也会从关联的数据表中删除该列。 此外，从 main 方法中删除列 `Fill` 会删除该 TableAdapter 的其他任何查询中的列。

可以使用 TableAdapter 查询配置向导为 TableAdapter 创建和编辑其他查询。 这些附加查询必须符合表架构，除非它们返回标量值。  每个其他查询都有你指定的名称。

以下示例演示如何调用名为 的其他查询 `FillByCity` ：

`CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, "Seattle")`

### <a name="to-start-the-tableadapter-query-configuration-wizard-with-a-new-query"></a>使用新查询启动 TableAdapter 查询配置向导

1. 在“数据集设计器”中打开数据集。

2. 如果要创建新查询，请将"工具箱"的"数据集"选项卡中的"查询"对象拖到上，或者从 TableAdapter 的快捷菜单中选择" <xref:System.Data.DataTable> 添加查询"。  还可以将 Query **对象拖动** 到 数据集设计器的空白区域，这将创建一个没有关联的 的 TableAdapter。 <xref:System.Data.DataTable> 这些查询只能返回单个 (标量) 值，或者对数据库运行 UPDATE、INSERT 或 DELETE 命令。

3. 在 **"选择数据连接"** 屏幕上，选择或创建查询将使用的连接。

    > [!NOTE]
    > 此屏幕仅在设计器无法确定使用的正确连接或没有可用连接时显示。

4. 在 **"选择命令类型"** 屏幕上，从以下从数据库提取数据的方法中选择：

    - **使用 SQL 语句**，可以键入 SQL 语句以从数据库中选择数据。

    - **创建新的存储过程使你** 能够让向导基于指定的 SELECT 语句在 (数据库中创建新的存储) 过程。

    - **使用现有存储过程** ，可以在运行查询时运行现有存储过程。

### <a name="to-start-the-tableadapter-query-configuration-wizard-on-an-existing-query"></a>对现有查询启动 TableAdapter 查询配置向导

- 如果要编辑现有的 TableAdapter 查询，请右键单击该查询，然后从 **快捷菜单中选择** "配置"。

    > [!NOTE]
    > 右键单击 TableAdapter 的主查询可重新配置 TableAdapter 和 <xref:System.Data.DataTable> 架构。 但是，右键单击 TableAdapter 上的附加查询只会配置所选查询。 **TableAdapter 配置向导** 重新配置 TableAdapter 定义，而 **TableAdapter 查询配置向导** 仅重新配置所选查询。

### <a name="to-add-a-global-query-to-a-tableadapter"></a>向 TableAdapter 添加全局查询

- 全局查询是SQL查询，这些查询返回单个 (标量) 值或无值。 通常，全局函数执行数据库操作，例如插入、更新和删除。 它们还聚合信息，例如表中的客户计数或特定订单中所有项的总费用。

     将"工具箱"的"数据集"选项卡中的 **"查询**"对象拖动到"工具箱"的空白区域，可以添加 **全局数据集设计器。**

- 提供执行所需任务的查询，例如 `SELECT COUNT(*) AS CustomerCount FROM Customers` 。

    > [!NOTE]
    > 将 Query **对象** 直接拖动到数据集设计器会创建一个方法，该方法仅返回单个 (标) 值。 尽管选择的查询或存储过程可能返回多个值，但向导创建的方法仅返回单个值。 例如，查询可能返回返回的数据的第一行的第一列。

## <a name="see-also"></a>请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
