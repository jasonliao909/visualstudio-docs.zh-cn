---
title: 使用 TableAdapter 直接访问数据库
description: 通过 TableAdapter 直接访问数据库，使用插入、更新和删除等方法直接在数据库中操作数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Visual Basic], accessing with a TableAdapter
- DBDirect methods
- datasets [Visual Basic], adding to projects
- data [Visual Studio], saving
- TableAdapter.Delete method
- GenerateDbDirectMethods property
- TableAdapter.Insert method
- TableAdapter.GenerateDBDirectMethods property
- TableAdapter.Update method
- saving data
- TableAdapters
ms.assetid: 012c5924-91f7-4790-b2a6-f51402b7014b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 18abf137354f6b5a752c217a68e7d70e74dd13fb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601167"
---
# <a name="directly-access-the-database-with-a-tableadapter"></a>使用 TableAdapter 直接访问数据库

除了 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 之外，还可使用能直接针对数据库运行的方法创建 TableAdapter。 可调用这些方法（`TableAdapter.Insert`、`TableAdapter.Update` 和 `TableAdapter.Delete`）来直接操作数据库中的数据。

如果不想创建这些直接方法，请在“属性”窗口中将 TableAdapter 的 `GenerateDbDirectMethods` 属性设置为 `false`。 除了 TableAdapter 的主要查询外，如果有任何查询添加到 TableAdapter，它们则是不会生成这些 `DbDirect` 方法的独立查询。

## <a name="send-commands-directly-to-a-database"></a>将命令直接发送到数据库

调用执行要尝试完成的任务的 `DbDirect` 方法。

### <a name="to-insert-new-records-directly-into-a-database"></a>将新记录直接插入数据库

- 调用 TableAdapter 的 `Insert` 方法，并将每列的值作为参数传入。 下面的过程以 Northwind 数据库中的 `Region` 表为例。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet15":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet15":::

### <a name="to-update-records-directly-in-a-database"></a>直接更新数据库中的记录

- 调用 TableAdapter 的 `Update` 方法，并将每列的新值和原始值作为参数传入。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet18":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet18":::

### <a name="to-delete-records-directly-from-a-database"></a>直接从数据库中删除记录

- 调用 TableAdapter 的 `Delete` 方法，并将每列的值作为 `Delete` 方法的参数传入。 下面的过程以 Northwind 数据库中的 `Region` 表为例。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet21":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet21":::

## <a name="see-also"></a>另请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
