---
title: 将新记录插入数据库
description: 使用 TableAdapter.Update 方法（TableAdapter 的 DBDirect 方法之一或命令对象）将新记录插入到数据库中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
ms.openlocfilehash: 7b3fbea039c82210c135b26c918ca18c757816b5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122113908"
---
# <a name="insert-new-records-into-a-database"></a>将新记录插入数据库

若要将新记录插入到数据库中，可以使用 方法或 TableAdapter 的 DBDirect 方法之一 (方法 `TableAdapter.Update` `TableAdapter.Insert`) 。 有关详细信息，请参阅 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

如果应用程序不使用 TableAdapters，可以使用命令对象 (例如，)  <xref:System.Data.SqlClient.SqlCommand> 在数据库中插入新记录。

如果应用程序使用数据集来存储数据，请使用 `TableAdapter.Update` 方法。 `Update`方法将所有更改 (更新、插入和删除) 数据库。

如果应用程序使用 对象来存储数据，或者希望更精细地控制在数据库中创建新记录，请使用 `TableAdapter.Insert` 方法。

如果 TableAdapter 没有方法，则意味着 TableAdapter 配置为使用存储过程，或者其 属性 `Insert` `GenerateDBDirectMethods` 设置为 `false` 。 尝试将 TableAdapter 的 属性从 数据集设计器 `GenerateDBDirectMethods` `true` 中，然后保存数据集。  这会重新生成 TableAdapter。 如果 TableAdapter 仍没有方法，则表可能未提供足够的架构信息来区分各个行 (例如，表行上可能未设置 `Insert`) 。

## <a name="insert-new-records-by-using-tableadapters"></a>使用 TableAdapters 插入新记录

TableAdapters 提供将新记录插入数据库的不同方法，具体取决于应用程序的要求。

如果应用程序使用数据集来存储数据，则只需将新记录添加到数据集中的所需记录， <xref:System.Data.DataTable> 然后调用 `TableAdapter.Update` 方法。 `TableAdapter.Update`方法将 中的任何更改发送到数据库 (包括已修改和 <xref:System.Data.DataTable> 已删除) 。

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>使用 TableAdapter.Update 方法将新记录插入数据库

1. 通过创建新的 并将其添加到集合 <xref:System.Data.DataTable> ，将新 <xref:System.Data.DataRow> 记录添加到 <xref:System.Data.DataTable.Rows%2A> 所需的 。

2. 将新行添加到 后 <xref:System.Data.DataTable> ，调用 `TableAdapter.Update` 方法。 可以通过传递整个 、、 、 数组或单个 来控制要 <xref:System.Data.DataSet> <xref:System.Data.DataTable> <xref:System.Data.DataRow> 更新的数据量 <xref:System.Data.DataRow> 。

   下面的代码演示如何将新记录添加到 ， <xref:System.Data.DataTable> 然后调用 `TableAdapter.Update` 方法将新行保存到数据库。  (此示例使用 `Region` Northwind database.) 中的 表

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form5.vb" id="Snippet14":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form5.cs" id="Snippet14":::

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>使用 TableAdapter.Insert 方法将新记录插入数据库

如果应用程序使用 对象来存储数据，可以使用 方法直接 `TableAdapter.Insert` 在数据库中创建新行。 `Insert`方法接受每列的单个值作为参数。 调用 方法会使用传入的参数值将新记录插入到数据库中。

- 调用 TableAdapter 的 方法，将每列 `Insert` 的值作为参数传递。

以下过程演示如何使用 `TableAdapter.Insert` 方法插入行。 此示例将数据插入到 `Region` Northwind 数据库中的 表中。

> [!NOTE]
> 如果没有可用的实例，请实例化想要使用的 TableAdapter。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet15":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet15":::

## <a name="insert-new-records-by-using-command-objects"></a>使用命令对象插入新记录

可以使用命令对象将新记录直接插入到数据库中。

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>使用命令对象将新记录插入数据库

- 创建新的命令对象，然后设置其 、 `Connection` `CommandType` 和 `CommandText` 属性。

下面的示例演示如何使用命令对象将记录插入数据库。 它将数据插入到 `Region` Northwind 数据库中的 表中。

:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet16":::
:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet16":::

## <a name="net-security"></a>.NET 安全性

您必须有权访问尝试连接到的数据库，以及执行插入到所需表中的操作的权限。

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
