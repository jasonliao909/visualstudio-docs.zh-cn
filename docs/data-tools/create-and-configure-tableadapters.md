---
title: 创建和配置 TableAdapter
description: 查看如何在 Visual Studio 中创建和配置 TableAdapter。 TableAdapter 提供应用程序与数据库之间的通信。
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
ms.openlocfilehash: 5f08a8c6d441a8b38f367ecfbdab95e1eabc113a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601187"
---
# <a name="create-and-configure-tableadapters"></a>创建和配置 TableAdapter

TableAdapter 提供应用程序与数据库之间的通信。 它们连接到数据库、运行查询或存储过程，并返回新数据表或使用返回的数据填充现有的 <xref:System.Data.DataTable>。 TableAdapter 还可将更新的数据从应用程序发送回数据库。

当你执行以下操作之一时，将为你创建 TableAdapter：

- 将数据库对象从“服务器资源管理器”拖动到“数据集设计器”中 。

- 运行数据源配置向导，然后选择“数据库”或“Web 服务”数据源类型 。

   ![Visual Studio 中的数据源配置向导](media/data-source-configuration-wizard.png)

你还可以创建新的 TableAdapter 并使用数据源对其进行配置，方法是将 TableAdapter 从“工具箱”拖动到“数据集设计器”图面的空白区域 。

有关 TableAdapter 的简介，请参阅[使用 TableAdapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="use-the-tableadapter-configuration-wizard"></a>使用 TableAdapter 配置向导

运行 TableAdapter 配置向导以创建或编辑 TableAdapter 及其关联的 DataTable。 可通过右键单击“数据集设计器”中现有的 TableAdapter 来对其进行配置。

![raddata TableAdapter 配置向导](../data-tools/media/raddata-table-adapter-configuration-wizard.png)

如果在数据集设计器位于焦点处时从工具箱拖动新的 TableAdapter，该向导会启动并提示你指定 TableAdapter 应连接到的数据源。 在下一页中，该向导会询问应使用哪种命令（SQL 语句或存储过程）与数据库进行通信。 （如果要配置的 TableAdapter 已经与数据源相关联，则不会显示此问题。）

- 如果对数据库具有正确的权限，则可以选择在基础数据库中创建新的存储过程。 如果没有这些权限，则无法选择此选项。

- 还可以选择为 TableAdapter 的 SELECT、INSERT、UPDATE 和 DELETE 命令运行现有的存储过程   。 例如，分配给 Update 命令的存储过程在调用 `TableAdapter.Update()` 方法时运行。

将参数从选中的存储过程映射到数据表中相应的列。 例如，如果存储过程接受一个传递到表中 `CompanyName` 列的名为 `@CompanyName` 的参数，则将 `@CompanyName` 参数的“源列”设置为 `CompanyName`。

> [!NOTE]
> 分配给 SELECT 命令的存储过程通过调用在向导的下一步中指定的 TableAdapter 的方法运行。 默认方法是 `Fill`，因此通常用于运行 SELECT 过程的代码是 `TableAdapter.Fill(tableName)`。 如果要更改 `Fill` 的默认名称，使用分配的名称替代 `Fill`，并将“TableAdapter”替换为 TableAdapter 的实际值（例如 `CustomersTableAdapter`）。

- 选择“创建方法以将更新直接发送到数据库”选项等效于将 `GenerateDBDirectMethods` 属性设置为 true。 当原始 SQL 语句未提供足够的信息或查询不是可更新的查询时，此选项不可用。 例如，JOIN 查询和返回单个（标量）值的查询中可能会出现这种情况。

使用向导中的“高级选项”可执行以下操作：

- 根据在“生成 SQL 语句”页上定义的 SELECT 语句生成 INSERT、UPDATE 和 DELETE 语句
- 使用开放式并发
- 指定是否在运行 INSERT 和 UPDATE 语句后刷新数据表

## <a name="configure-a-tableadapters-fill-method"></a>配置 TableAdapter 的 Fill 方法

有时，你可能需要更改 TableAdapter 的表架构。 为此，需修改 TableAdapter 的主要 `Fill` 方法。 TableAdapter 是使用主要 `Fill` 方法创建的，该方法可定义关联数据表的架构。 主要 `Fill` 方法基于最初配置 TableAdapter 时输入的查询或存储过程。 它是数据集设计器中数据表下的首个（最顶端的）方法。

![带有多个查询的 TableAdapter](../data-tools/media/tableadapter.gif)

对 TableAdapter 的主要 `Fill` 方法所做的任何更改都会反映在关联数据表的架构中。 例如，从主要 `Fill` 方法的查询中删除某个列也会将关联数据表中的该列删除。 此外，从主要 `Fill` 方法中删除该列会将该 TableAdapter 的任何附加查询的该列删除。

可以使用 TableAdapter 查询配置向导为 TableAdapter 创建和编辑附加查询。 这些附加查询必须符合表架构，除非它们返回标量值。  每个附加查询都具有指定的名称。

以下示例显示如何调用名为 `FillByCity` 的附加查询：

`CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, "Seattle")`

### <a name="to-start-the-tableadapter-query-configuration-wizard-with-a-new-query"></a>通过新查询启动 TableAdapter 查询配置向导

1. 在“数据集设计器”中打开数据集。

2. 如果要创建新查询，将“查询”对象从“工具箱”的“数据集”选项卡拖动到 <xref:System.Data.DataTable> 上，或从 TableAdapter 的快捷菜单中选择“添加查询”   。 还可以将“查询”对象拖动到“数据集设计器”的空白区域中，这会创建不具有关联 <xref:System.Data.DataTable> 的 TableAdapter 。 这些查询只能返回单个（标量）值，或针对数据库运行 UPDATE、INSERT 或 DELETE 命令。

3. 在“选择你的数据连接”屏幕上，选择或创建查询将使用的连接。

    > [!NOTE]
    > 仅当设计器无法确定要使用的正确连接或无可用连接时，此屏幕才会显示。

4. 在“选择命令类型”屏幕上，选择以下从数据库提取数据的方法：

    - 可以通过“使用 SQL 语句”键入 SQL 语句，以从数据库中选择数据。

    - 可以通过“创建新存储过程”使向导根据指定的 SELECT 语句创建新的存储过程（在数据库中）。

    - 可以通过“使用现有存储过程”在运行查询时运行现有的存储过程。

### <a name="to-start-the-tableadapter-query-configuration-wizard-on-an-existing-query"></a>在现有查询上启动 TableAdapter 查询配置向导

- 如果要编辑现有的 TableAdapter 查询，右键单击该查询，然后从快捷菜单中选择“配置”。

    > [!NOTE]
    > 右键单击 TableAdapter 的主查询可重新配置 TableAdapter 和 <xref:System.Data.DataTable> 架构。 但是，右键单击 TableAdapter 上的其他查询时，仅可配置所选查询。 TableAdapter 配置向导重新配置 TableAdapter 定义，而 TableAdapter 查询配置向导仅重新配置所选的查询 。

### <a name="to-add-a-global-query-to-a-tableadapter"></a>向 TableAdapter 添加全局查询

- 全局查询是返回单个（标量）值或不返回值的 SQL 查询。 通常，全局函数执行插入、更新和删除等数据库操作。 它们还聚合信息，例如表中的客户计数或按特定顺序排列的所有项的总费用。

     通过将“查询”对象从“工具箱”的“数据集”选项卡拖动到“数据集设计器”的空白区域中，添加全局查询   。

- 提供可执行所需任务的查询，例如 `SELECT COUNT(*) AS CustomerCount FROM Customers`。

    > [!NOTE]
    > 将“查询”对象直接拖动到“数据集设计器”可创建仅返回标量（单个）值的方法 。 尽管所选的查询或存储过程可能会返回多个值，但向导创建的方法只返回单个值。 例如，查询可能返回返回的数据的第一行第一列。

## <a name="see-also"></a>另请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
