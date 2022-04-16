---
title: 将新记录插入数据库
description: 使用 TableAdapter.Update 方法、TableAdapter 的 DBDirect 方法之一或命令对象将新记录插入到数据库中。
ms.custom: SEO-VS-2020
ms.date: 04/12/2022
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, inserting new records into
- data [Visual Studio], saving
- databases, inserting new records into
- records, inserting
- saving data
ms.assetid: ea118fff-69b1-4675-b79a-e33374377f04
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 06ef7371a0da841a148eb417abb32daac07b1805
ms.sourcegitcommit: 02b5dbdec3ae86c3dfb8c15344a2c195db7b424a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2022
ms.locfileid: "142645918"
---
# <a name="insert-new-records-into-a-database"></a>将新记录插入数据库

若要在.NET Framework项目中将新记录插入 [ADO.NET](/dotnet/framework/data/adonet/) 的数据库，可以使用该方法`TableAdapter.Update`或 TableAdapter 的 DBDirect 方法之一，具体`TableAdapter.Insert` (该方法) 。 有关详细信息，请参阅 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

如果应用程序不使用 TableAdapters，你可以使用命令对象（例如 <xref:System.Data.SqlClient.SqlCommand>）将新记录插入数据库。

如果应用程序使用数据集来存储数据，请使用 `TableAdapter.Update` 方法。 `Update` 方法将所有更改（更新、插入和删除）发送到数据库。

如果应用程序使用对象来存储数据，或者你想要更精细地控制如何在数据库中新建记录，请使用 `TableAdapter.Insert` 方法。

如果 TableAdapter 没有 `Insert` 方法，则意味着 TableAdapter 配置为使用存储过程或其 `GenerateDBDirectMethods` 属性设置为 `false`。 尝试在数据集设计器中将 TableAdapter 的 `GenerateDBDirectMethods` 属性设置为 `true`，然后保存数据集。 这将重新生成 TableAdapter。 如果 TableAdapter 仍然没有 `Insert` 方法，则表可能没有提供足够的架构信息来区分各个行（例如，表上可能没有设置主键）。

> [!NOTE]
> 本文适用于 ADO.NET 和.NET Framework开发。 有关 Entity Framework 6 的相同任务，请参阅 [向上下文添加新实体](/ef/ef6/saving/change-tracking/entity-state#adding-a-new-entity-to-the-context)。 有关 Entity Framework Core，请参阅 [添加数据](/ef/core/saving/basic#adding-data)。

## <a name="insert-new-records-by-using-tableadapters"></a>使用 TableAdapters 插入新记录

根据应用程序的需求，TableAdapter 提供了将新记录插入数据库的不同方法。

如果应用程序使用数据集来存储数据，则你只需将新记录添加到数据集中所需的 <xref:System.Data.DataTable>，然后调用 `TableAdapter.Update` 方法。 `TableAdapter.Update` 方法将 <xref:System.Data.DataTable> 中的所有更改发送到数据库（包括修改和删除的记录）。

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>使用 TableAdapter.Update 方法将新记录插入数据库

1. 通过新建 <xref:System.Data.DataRow> 并将其添加到 <xref:System.Data.DataTable.Rows%2A> 集合，将新记录添加到所需的 <xref:System.Data.DataTable>。

2. 将新行添加到 <xref:System.Data.DataTable> 后，调用 `TableAdapter.Update` 方法。 可以通过传入整个 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> 数组或单个 <xref:System.Data.DataRow> 来控制要更新的数据量。

   以下代码显示如何向 <xref:System.Data.DataTable> 添加新记录，然后调用 `TableAdapter.Update` 方法将新行保存到数据库。 （该示例使用 Northwind 数据库中的 `Region` 表。）

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form5.vb" id="Snippet14":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form5.cs" id="Snippet14":::

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>使用 TableAdapter.Insert 方法将新记录插入数据库

如果应用程序使用对象来存储数据，你可以使用 `TableAdapter.Insert` 方法直接在数据库中新建行。 `Insert` 方法可接受每列的各个值作为参数。 调用该方法会将新记录插入数据库，并传入参数值。

- 调用 TableAdapter 的 `Insert` 方法，并将每列的值作为参数传入。

以下过程演示如何使用 `TableAdapter.Insert` 方法插入行。 本示例将数据插入 Northwind 数据库的 `Region` 表。

> [!NOTE]
> 如果没有可用的实例，请实例化要使用的 TableAdapter。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet15":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet15":::

## <a name="insert-new-records-by-using-command-objects"></a>使用命令对象插入新记录

可以使用命令对象将新记录直接插入数据库。

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>使用命令对象将新记录插入数据库

- 新建命令对象，然后设置其 `Connection`、`CommandType` 和 `CommandText` 属性。

以下示例演示如何使用命令对象将记录插入数据库。 该示例将数据插入 Northwind 数据库的 `Region` 表。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet16":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet16":::

## <a name="net-security"></a>.NET 安全性

必须有权访问尝试连接的数据库，且有权对所需表执行插入操作。

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
