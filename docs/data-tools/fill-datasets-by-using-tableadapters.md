---
title: 使用 Tableadapter 填充数据集
description: 使用 TableAdapters 填充数据集。 TableAdapter 组件根据指定的一个或多个查询或存储过程，使用来自 DB 的数据填充数据集。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic]
- datasets [Visual Basic], loading data
- data retrieval
- retrieving data
- datasets [Visual Basic], filling
- data [Visual Studio], retrieving
- data [Visual Studio], datasets
ms.assetid: 55f3bfbe-db78-4486-add3-c62f49e6b9a0
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 70013e4943e256871dfe12e38b364da1cc67c94f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122036948"
---
# <a name="fill-datasets-by-using-tableadapters"></a>使用 Tableadapter 填充数据集

TableAdapter 组件根据指定的一个或多个查询或存储过程，使用数据库中的数据填充数据集。 TableAdapters 还可以对数据库执行添加、更新和删除操作，以保留对数据集所做的更改。 还可以发出与任何特定表无关的全局命令。

> [!NOTE]
> TableAdapters 由Visual Studio生成。 如果要以编程方式创建数据集，请使用 DataAdapter，这是一个 .NET 类。

有关 TableAdapter 操作的详细信息，可以直接跳到以下主题之一：

|主题|说明|
|-----------|-----------------|
|[创建和配置 TableAdapter](../data-tools/create-and-configure-tableadapters.md)|如何使用设计器创建和配置 TableAdapters|
|[创建参数化 TableAdapter 查询](../data-tools/create-parameterized-tableadapter-queries.md)|如何让用户向 TableAdapter 过程或查询提供参数|
|[使用 TableAdapter 直接访问数据库](../data-tools/directly-access-the-database-with-a-tableadapter.md)|如何使用 TableAdapters 的 Dbdirect 方法|
|[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)|更新数据时如何使用外键约束|
|[如何：扩展 TableAdapter 的功能](../data-tools/fill-datasets-by-using-tableadapters.md)|如何将自定义代码添加到 TableAdapters|
|[将 XML 数据读入到数据集中](../data-tools/read-xml-data-into-a-dataset.md)|如何使用 XML|

<a name="tableadapter-overview"></a>

## <a name="tableadapter-overview"></a>TableAdapter 概述

TableAdapters 是设计器生成的组件，用于连接到数据库、运行查询或存储过程，以及使用返回的数据填充其 DataTable。 TableAdapters 还会将更新后的数据从应用程序发送回数据库。 只要 TableAdapter 返回的数据符合 TableAdapter 所关联的表的架构，就可以对 TableAdapter 运行任何多的查询。 下图显示了 TableAdapters 如何与内存中的数据库和其他对象交互：

![客户端应用程序中的数据流](../data-tools/media/clientdatadiagram.gif)

虽然 TableAdapter 是使用数据集设计器设计的，但 TableAdapter 类不会生成为 的嵌套类 <xref:System.Data.DataSet> 。 它们位于特定于每个数据集的单独命名空间中。 例如，如果有一个名为 的数据集，则 与 中的 `NorthwindDataSet` 关联的 TableAdapters  <xref:System.Data.DataTable> `NorthwindDataSet` 将放在 `NorthwindDataSetTableAdapters` 命名空间中。 若要以编程方式访问特定的 TableAdapter，必须声明 TableAdapter 的新实例。 例如：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Class1.cs" id="Snippet7":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Class1.vb" id="Snippet7":::

## <a name="associated-datatable-schema"></a>关联的 DataTable 架构

创建 TableAdapter 时，可以使用初始查询或存储过程来定义 TableAdapter 的关联 的架构 <xref:System.Data.DataTable> 。 通过调用 TableAdapter 的 方法来运行此初始查询或存储过程 (该方法将填充 `Fill` TableAdapter 的关联 <xref:System.Data.DataTable>) 。 对 TableAdapter 的主查询进行的任何更改都反映在关联数据表的架构中。 例如，从主查询中删除列也会从关联的数据表中删除该列。 如果 TableAdapter 上任何其他查询都使用返回不在主查询中的列的 SQL 语句，设计器将尝试同步主查询和其他查询之间的列更改。

## <a name="tableadapter-update-commands"></a>TableAdapter 更新命令

TableAdapter 的更新功能取决于 **TableAdapter** 向导 的主查询中有多少信息可用。 例如，配置为使用) 从多个表提取值的 TableAdapters (最初不会创建标量值、视图或聚合函数的结果，无法将更新发送回 `JOIN` 基础数据库。 但是，可以在"属性"窗口中手动配置 `INSERT` `UPDATE` 、 `DELETE` **和** 命令。

## <a name="tableadapter-queries"></a>TableAdapter 查询

![带有多个查询的 TableAdapter](../data-tools/media/tableadapter.gif)

TableAdapters 可以包含多个查询来填充其关联的数据表。 只要每个查询返回的数据符合与其关联的数据表相同的架构，就可以为 TableAdapter 定义应用程序所需的查询数。 此功能使 TableAdapter 能够根据不同的条件加载不同的结果。

例如，如果应用程序包含一个包含客户名称的表，可以创建一个查询，该查询使用以特定字母开头的每一个客户名称填充该表，创建一个查询，该查询用位于同一状态的所有客户填充该表。 若要向具有给定状态的客户填充表，可以创建一个查询，该查询采用状态 `Customers` `FillByState` 值的参数，如下所示 `SELECT * FROM Customers WHERE State = @State` ：。 通过调用 方法并传递如下所示的参数值 `FillByState` 来运行查询 `CustomerTableAdapter.FillByState("WA")` ：。

除了添加返回 TableAdapter 数据表相同架构数据的查询外，还可以添加返回标量值 (单个) 查询。 例如，返回客户计数 () 即使返回的数据不符合表的架构，该查询对 `SELECT Count(*) From Customers` `CustomersTableAdapter,` 也有效。

## <a name="clearbeforefill-property"></a>ClearBeforeFill 属性

默认情况下，每次运行查询来填充 TableAdapter 的数据表时，都会清除现有数据，并且仅将查询结果加载到表中。 如果要将查询返回的数据添加或合并到数据表中的现有数据，将 TableAdapter 的 `ClearBeforeFill` `false` 属性设置为 。 无论是否清除数据，如果要保留更新，都需要将更新显式发送回数据库。 因此，在运行填充表的另一个查询之前，请记住保存对表中的数据的任何更改。 有关详细信息，请参阅使用 [TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。

## <a name="tableadapter-inheritance"></a>TableAdapter 继承

TableAdapters 通过封装配置的类来扩展标准数据适配器 <xref:System.Data.Common.DataAdapter> 的功能。 默认情况下，TableAdapter 继承自 <xref:System.ComponentModel.Component> 类，不能强制转换到 <xref:System.Data.Common.DataAdapter> 类。 将 TableAdapter 强制 <xref:System.Data.Common.DataAdapter> 转换到 类会导致 <xref:System.InvalidCastException> 错误。 若要更改 TableAdapter 的基类，可以在 表的 TableAdapter 的基类属性中指定派生自 的 <xref:System.ComponentModel.Component> **类** 数据集设计器。 

## <a name="tableadapter-methods-and-properties"></a>TableAdapter 方法和属性

TableAdapter 类不是 .NET 类型。 这意味着你无法查看文档或对象 **浏览器**。 它是在设计时创建的，使用前面提到的向导之一。 创建 TableAdapter 时分配给它的名称基于所处理表的名称。 例如，在基于名为 的数据库中的表创建 `Orders` TableAdapter 时，TableAdapter 命名为 `OrdersTableAdapter` 。 可以使用表 中的 Name 属性更改 TableAdapter的类 **数据集设计器。**

下面是 TableAdapters 的常用方法和属性：

|成员|说明|
|------------|-----------------|
|`TableAdapter.Fill`|使用 TableAdapter 命令的结果填充 TableAdapter 的关联数据 `SELECT` 表。|
|`TableAdapter.Update`|将更改发送回数据库并返回一个整数，该整数表示受更新影响的行数。 有关详细信息，请参阅使用 [TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。|
|`TableAdapter.GetData`|返回填充 <xref:System.Data.DataTable> 了数据的新 。|
|`TableAdapter.Insert`|在数据表中创建新行。 有关详细信息，请参阅 [将新记录插入数据库](../data-tools/insert-new-records-into-a-database.md)。|
|`TableAdapter.ClearBeforeFill`|确定在调用方法之一之前是否清空数据 `Fill` 表。|

## <a name="tableadapter-update-method"></a>TableAdapter 更新方法

TableAdapters 使用数据命令读取和写入数据库。 使用 TableAdapter (main) 查询作为创建关联数据表的架构以及与 方法关联的 、 和 命令 `Fill` `InsertCommand` `UpdateCommand` `DeleteCommand` `TableAdapter.Update` 的基础。 调用 TableAdapter 的 方法将运行最初配置 TableAdapter 时创建的语句，而不是使用 `Update` **TableAdapter** 查询配置向导 添加的其他查询之一。

使用 TableAdapter 时，它使用通常会执行的命令有效地执行相同的操作。 例如，调用适配器的 方法时，适配器在其 属性中运行数据命令，并使用数据读取器 (例如，) 将结果集加载到数据 `Fill` `SelectCommand` <xref:System.Data.SqlClient.SqlDataReader> 表中。 同样，调用适配器的 方法时，它会在 、 (属性中运行相应的命令，) 表中每个已更改的记录 `Update` `UpdateCommand` `InsertCommand` `DeleteCommand` 。

> [!NOTE]
> 如果主查询中有足够的信息，则生成 `InsertCommand` TableAdapter 时，默认情况下会 `UpdateCommand` 创建 、 和 `DeleteCommand` 命令。 如果 TableAdapter 的主查询不止一个表语句，则设计器可能无法生成 `SELECT` `InsertCommand` 、 和 `UpdateCommand` `DeleteCommand` 。 如果未生成这些命令，则运行 方法时可能会收到 `TableAdapter.Update` 错误。

## <a name="tableadapter-generatedbdirectmethods"></a>TableAdapter GenerateDbDirectMethods

除了 、 和 之外，还使用可以直接针对数据库运行的方法创建 `InsertCommand` `UpdateCommand` `DeleteCommand` TableAdapters。 可以直接调用 、 (和 `TableAdapter.Insert` `TableAdapter.Update` `TableAdapter.Delete`) 来操作数据库中的数据。 这意味着可以从代码中调用这些单独的方法，而不是调用 来处理挂起的关联数据表 `TableAdapter.Update` 的插入、更新和删除。

如果不想创建这些直接方法，请设置 TableAdapter 的 **GenerateDbDirectMethods** 属性， ("属性 `false` "窗口中) 。  添加到 TableAdapter 的其他查询是独立查询 - 它们不会生成这些方法。

## <a name="tableadapter-support-for-nullable-types"></a>TableAdapter 对可为空类型的支持

TableAdapters 支持可为空类型和 `Nullable(Of T)` `T?` 。 若要深入了解 Visual Basic 中可以为 null 的类型，请参阅[可以为 null 的值类型](/dotnet/visual-basic/programming-guide/language-features/data-types/nullable-value-types)。 有关 C# 中可为空类型的信息，请参阅 [使用可为空类型](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。

<a name="tableadaptermanager-reference"></a>

## <a name="tableadaptermanager-reference"></a>TableAdapterManager 参考

默认情况下，创建包含相关表的数据集时，将生成 TableAdapterManager 类。 若要防止生成类，请将数据集的 属性的值更改为 `Hierarchical Update` false。 将具有关系的表拖动到窗体或 WPF Windows的设计图面上时，Visual Studio声明 类的成员变量。 如果不使用数据绑定，必须手动声明变量。

TableAdapterManager 类不是 .NET 类型。 因此，无法在文档中查找它。 它是在设计时作为数据集创建过程的一部分创建的。

以下是 类的常用方法和 `TableAdapterManager` 属性：

|成员|说明|
|------------|-----------------|
|`UpdateAll` 方法|保存所有数据表中的所有数据。|
|`BackUpDataSetBeforeUpdate` 属性|确定是否在执行 方法之前创建数据集的备份 `TableAdapterManager.UpdateAll` 副本。布尔。|
|*tableName* `TableAdapter` 财产|表示 TableAdapter。 生成的 TableAdapterManager 包含它所管理的每个 `TableAdapter` 属性。 例如，包含 Customers 和 Orders 表的数据集使用包含 和 属性的 TableAdapterManager `CustomersTableAdapter` `OrdersTableAdapter` 生成。|
|`UpdateOrder` 属性|控制单个插入、更新和删除命令的顺序。 将此选项设置为 枚举中的值 `TableAdapterManager.UpdateOrderOption` 之一。<br /><br /> 默认情况下， `UpdateOrder` 设置为 **InsertUpdateDelete**。 这意味着，对数据集中所有表执行插入、更新和删除操作。|

## <a name="security"></a>安全性

使用 CommandType 属性设置为 的数据命令时，请仔细检查从客户端发送的信息，然后再 <xref:System.Data.CommandType.Text> 将该信息传递到数据库。 恶意用户会设法发送（注入）经过修改或附加的 SQL 语句，企图对数据库进行未经授权的访问或破坏数据库。 将用户输入传输至数据库之前，请始终验证信息是否有效。 最佳做法是尽可能始终使用参数化查询或存储过程。

## <a name="see-also"></a>请参阅

- [数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
