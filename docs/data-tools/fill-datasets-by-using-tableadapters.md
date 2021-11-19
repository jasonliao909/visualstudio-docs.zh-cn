---
title: 使用 Tableadapter 填充数据集
description: 使用 Tableadapter 填充数据集。 TableAdapter 组件基于指定的一个或多个查询或存储过程，用数据库中的数据填充数据集。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601158"
---
# <a name="fill-datasets-by-using-tableadapters"></a>使用 Tableadapter 填充数据集

TableAdapter 组件基于指定的一个或多个查询或存储过程，用数据库中的数据填充数据集。 Tableadapter 还可对数据库执行添加、更新和删除操作，以便保留对数据集所做的更改。 还可发出与任何特定表无关的全局命令。

> [!NOTE]
> TableAdapters 由 Visual Studio 设计器生成。 如果要以编程方式创建数据集，请使用 DataAdapter，这是一个 .NET 类。

有关 TableAdapter 操作的详细信息，可直接跳到以下主题之一：

|主题|说明|
|-----------|-----------------|
|[创建和配置 TableAdapter](../data-tools/create-and-configure-tableadapters.md)|如何使用设计器创建和配置 TableAdapter|
|[创建参数化 TableAdapter 查询](../data-tools/create-parameterized-tableadapter-queries.md)|如何使用户能够为 TableAdapter 过程或查询提供参数|
|[使用 TableAdapter 直接访问数据库](../data-tools/directly-access-the-database-with-a-tableadapter.md)|如何使用 Tableadapter 的 Dbdirect 方法|
|[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)|如何在更新数据时使用外键约束|
|[如何：扩展 TableAdapter 的功能](../data-tools/fill-datasets-by-using-tableadapters.md)|如何将自定义代码添加到 Tableadapter|
|[将 XML 数据读入到数据集中](../data-tools/read-xml-data-into-a-dataset.md)|如何使用 XML|

<a name="tableadapter-overview"></a>

## <a name="tableadapter-overview"></a>TableAdapter 概述

Tableadapter 是由设计器生成的组件，可连接到数据库、运行查询或存储过程，还可使用返回的数据填充其数据表。 Tableadapter 还会将更新后的数据从应用程序发送回数据库。 可在 TableAdapter 上运行任意多个查询，前提是这些查询返回的数据符合与 TableAdapter 关联的表的架构。 下图显示了 Tableadapter 如何与数据库和内存中的其他对象进行交互：

![客户端应用程序中的数据流](../data-tools/media/clientdatadiagram.gif)

虽然 TableAdapter 是使用数据集设计器设计的，但 TableAdapter 类并不作为 <xref:System.Data.DataSet> 的嵌套类生成。 它们位于特定于每个数据集的单独命名空间中。 例如，如果你有一个名为 `NorthwindDataSet` 的数据集，则与 `NorthwindDataSet` 中的 <xref:System.Data.DataTable> 关联的 TableAdapters 将位于 `NorthwindDataSetTableAdapters` 命名空间中。 若要以编程方式访问特定 TableAdapter，必须声明 TableAdapter 的新实例。 例如：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Class1.cs" id="Snippet7":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Class1.vb" id="Snippet7":::

## <a name="associated-datatable-schema"></a>关联的 DataTable 架构

创建 TableAdapter 时，使用初始查询或存储过程来定义 TableAdapter 关联的 <xref:System.Data.DataTable> 的架构。 可调用 TableAdapter 的 `Fill` 方法（它会填充 TableAdapter 关联的 <xref:System.Data.DataTable>）来运行此初始查询或存储过程。 对 TableAdapter 的主查询所做的任何更改都会反映在关联数据表的架构中。 例如，从主查询中删除列也会将关联的数据表中的对应列删除。 如果 TableAdapter 上的任何附加查询使用 SQL 语句返回主查询中没有的列，则设计器将尝试同步主查询与附加查询之间的列更改。

## <a name="tableadapter-update-commands"></a>TableAdapter 更新命令

TableAdapter 的更新功能取决于 TableAdapter 向导中的主查询中提供了多少信息。 例如，如果 Tableadapter 配置为从多个表中提取值（使用 `JOIN`）、标量值、视图或聚合函数的结果，则最初不会创建可将更新发送回基础数据库的功能。 但是，可在属性窗口中手动配置 `INSERT`、`UPDATE` 和 `DELETE` 命令。

## <a name="tableadapter-queries"></a>TableAdapter 查询

![带有多个查询的 TableAdapter](../data-tools/media/tableadapter.gif)

Tableadapter 可包含多个查询来填充关联的数据表。 可根据应用程序的需要为 TableAdapter 定义任意多个查询，前提是每个查询都返回与其关联数据表具有相同架构的数据。 此功能使 TableAdapter 能够根据不同的条件加载不同的结果。

例如，如果应用程序中有一个包含客户名称的表，则可创建一个查询，使用以特定字母开头的每个客户名称来填充该表，再创建另一个查询，使用位于同一州的所有客户填充该表。 若要使用位于特定州的客户填充 `Customers` 表，可创建一个 `FillByState` 查询，将一个参数用作州值，如下所示：`SELECT * FROM Customers WHERE State = @State`。 可通过调用 `FillByState` 方法并传入参数值来运行查询，如下所示：`CustomerTableAdapter.FillByState("WA")`。

除了添加查询来返回与 TableAdapter 的数据表具有相同架构的数据外，还可添加返回标量（单个）值的查询。 例如，即使返回的数据不符合表的架构，返回客户计数的查询 (`SELECT Count(*) From Customers`) 对 `CustomersTableAdapter,` 来说也是有效的。

## <a name="clearbeforefill-property"></a>ClearBeforeFill 属性

默认情况下，每次运行查询来填充 TableAdapter 的数据表时，现有数据都会被清除，并且仅将查询的结果加载到表中。 如果要将从查询返回的数据添加或合并到数据表中的现有数据，请将 TableAdapter 的 `ClearBeforeFill` 属性设置为 `false`。 不管是否清除数据，都需要将更新显式发送回数据库（如果要保留这些更新）。 因此，请记得在运行填充表的另一个查询之前，保存对表中数据所做的任何更改。 有关详细信息，请参阅[使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。

## <a name="tableadapter-inheritance"></a>TableAdapter 继承

Tableadapter 通过封装配置的 <xref:System.Data.Common.DataAdapter> 类来扩展标准数据适配器的功能。 默认情况下，TableAdapter 从 <xref:System.ComponentModel.Component> 类继承，且不能强制转换为 <xref:System.Data.Common.DataAdapter> 类。 将 TableAdapter 强制转换为 <xref:System.Data.Common.DataAdapter> 类会导致 <xref:System.InvalidCastException> 错误。 若要更改 TableAdapter 的基类，可在数据集设计器的 TableAdapter 的 Base Class 属性中指定从 <xref:System.ComponentModel.Component> 派生的类 。

## <a name="tableadapter-methods-and-properties"></a>TableAdapter 方法和属性

TableAdapter 类不是 .NET 类型。 这意味着不能在文档或对象浏览器中查找它。 它是在设计时，使用前面提到的其中一个向导创建的。 创建时分配给 TableAdapter 的名称基于你正在使用的表的名称。 例如，基于名为 `Orders` 的数据库中的表创建 TableAdapter 时，TableAdapter 将命名为 `OrdersTableAdapter`。 可使用数据集设计器中的 Name 属性更改 TableAdapter 的类名 。

下面是 Tableadapter 的常用方法和属性：

|成员|说明|
|------------|-----------------|
|`TableAdapter.Fill`|用 TableAdapter 的 `SELECT` 命令的结果填充 TableAdapter 的关联数据表。|
|`TableAdapter.Update`|将更改发送回数据库，并返回一个整数，该整数表示受更新影响的行数。 有关详细信息，请参阅[使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)。|
|`TableAdapter.GetData`|返回填充了数据的新的 <xref:System.Data.DataTable>。|
|`TableAdapter.Insert`|在数据表中创建新行。 有关详细信息，请参阅[在数据库中插入新记录](../data-tools/insert-new-records-into-a-database.md)。|
|`TableAdapter.ClearBeforeFill`|确定在调用 `Fill` 方法之前是否清空了数据表。|

## <a name="tableadapter-update-method"></a>TableAdapter 更新方法

Tableadapter 使用数据命令从数据库中读取数据和向其写入数据。 以 TableAdapter 的初始 `Fill`（主）查询为基础来创建关联数据表的架构，并将该查询用作与 `TableAdapter.Update` 方法关联的 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 命令。 调用 TableAdapter 的 `Update` 方法会运行最初配置 TableAdapter 时创建的语句，而不是运行使用“TableAdapter 查询配置向导”添加的其他任一查询。

使用 TableAdapter 时，它会有效地执行与通常会执行的命令相同的操作。 例如，调用适配器的 `Fill` 方法时，适配器会在其 `SelectCommand` 属性中运行数据命令，并使用数据读取器（例如 <xref:System.Data.SqlClient.SqlDataReader>）将结果集加载到数据表。 同样，在调用适配器的 `Update` 方法时，它会为数据表中的每个更改记录运行适当的命令（在 `UpdateCommand`、`InsertCommand` 和 `DeleteCommand` 属性中）。

> [!NOTE]
> 如果主查询中有足够的信息，则默认情况下，在生成 TableAdapter 时，会创建 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 命令。 如果 TableAdapter 的主查询不仅仅是单个表 `SELECT` 语句，则设计器可能无法生成 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand`。 如果未生成这些命令，则在运行 `TableAdapter.Update` 方法时可能会收到错误。

## <a name="tableadapter-generatedbdirectmethods"></a>TableAdapter GenerateDbDirectMethods

除了 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 之外，还可使用能直接针对数据库运行的方法创建 TableAdapter。 可直接调用这些方法（`TableAdapter.Insert`、`TableAdapter.Update` 和 `TableAdapter.Delete`）来操作数据库中的数据。 这意味着你可从代码中调用这些单独的方法，而不是调用 `TableAdapter.Update` 来处理对关联数据表挂起的插入、更新和删除操作。

如果不想创建这些直接方法，请在属性窗口中将 TableAdapter 的 GenerateDbDirectMethods 属性设置为 `false` 。 添加到 TableAdapter 的其他查询是独立查询，它们不会生成这些方法。

## <a name="tableadapter-support-for-nullable-types"></a>TableAdapter 支持可以为 null 的类型

TableAdapter 支持可以为 null 的类型 `Nullable(Of T)` 和 `T?`。 若要深入了解 Visual Basic 中可以为 null 的类型，请参阅[可以为 null 的值类型](/dotnet/visual-basic/programming-guide/language-features/data-types/nullable-value-types)。 若要详细了解 C# 中可以为 null 的类型，请参阅[使用可以为 null 的类型](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。

<a name="tableadaptermanager-reference"></a>

## <a name="tableadaptermanager-reference"></a>TableAdapterManager 引用

默认情况下，创建包含相关表的数据集时，会生成 TableAdapterManager 类。 若要防止生成该类，请将数据集的 `Hierarchical Update` 属性的值更改为 false。 将具有关系的表拖到 Windows 窗体或 WPF 页面的设计图面上时，Visual Studio 会声明该类的一个成员变量。 如果不使用数据绑定，则必须手动声明该变量。

TableAdapterManager 类不是 .NET 类型。 因此，无法在文档中查找它。 它是在创建数据集的过程中进行设计时创建的。

以下是 `TableAdapterManager` 类的常用方法和属性：

|成员|说明|
|------------|-----------------|
|`UpdateAll` 方法|保存所有数据表中的所有数据。|
|`BackUpDataSetBeforeUpdate` 属性|确定是否在执行 `TableAdapterManager.UpdateAll` 方法之前创建数据集的备份副本。布尔。|
|tableName `TableAdapter` 属性|表示 TableAdapter。 生成的 TableAdapterManager 包含其管理的每个 `TableAdapter` 的属性。 例如，具有 Customers 和 Orders 表的数据集将生成包含 `CustomersTableAdapter` 和 `OrdersTableAdapter` 属性的 TableAdapterManager。|
|`UpdateOrder` 属性|控制单个插入、更新和删除命令的顺序。 将此项设置为 `TableAdapterManager.UpdateOrderOption` 枚举中的值之一。<br /><br /> 默认情况下，`UpdateOrder` 设置为 InsertUpdateDelete。 这意味着，对数据集中所有表依次执行插入、更新和删除操作。|

## <a name="security"></a>安全性

当使用 CommandType 属性设置为 <xref:System.Data.CommandType.Text> 的数据命令时，请仔细检查从客户端发送的信息，然后再将其传递到数据库。 恶意用户会设法发送（注入）经过修改或附加的 SQL 语句，企图对数据库进行未经授权的访问或破坏数据库。 在将用户输入传输到数据库之前，始终要验证信息是否有效。 最佳做法是尽可能使用参数化查询或存储过程。

## <a name="see-also"></a>另请参阅

- [数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
