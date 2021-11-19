---
title: 将数据从对象保存到数据库
description: 使用 Visual Studio 中的数据集工具将数据从对象保存到数据库。 了解如何保存新记录、更新现有记录以及删除现有记录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 96e296be3bb5e591f3da9699fe15371659dddfc0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601102"
---
# <a name="save-data-from-an-object-to-a-database"></a>将数据从对象保存到数据库

通过将对象中的值传递给 TableAdapter 的 DBDirect 方法之一（例如 `TableAdapter.Insert`），可以将对象中的数据保存到数据库中。 有关详细信息，请参阅 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

若要从对象集合保存数据，请循环访问对象集合（例如 for-next 循环），然后使用 TableAdapter 的 `DBDirect` 方法之一将每个对象的值发送到数据库。

默认情况下，`DBDirect` 方法是在可直接针对数据库运行的 TableAdapter 上创建的。 这些方法可直接进行调用，并且不需要 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 对象来协调更改，以便向数据库发送更新。

> [!NOTE]
> 配置 TableAdapter 时，主查询必须提供足够的信息，以便创建 `DBDirect` 方法。 例如，如果将 TableAdapter 配置为从未定义主键列的表中查询数据，则它不会生成 `DBDirect` 方法。

|TableAdapter DBDirect 方法|说明|
| - |-----------------|
|`TableAdapter.Insert`|将新记录添加到数据库，使你可以将单个列值作为方法参数传入。|
|`TableAdapter.Update`|更新数据库中的现有记录。 `Update` 方法采用原始列值和新列值作为方法参数。 原始值用于查找原始记录，新值用于更新该记录。<br /><br /> `TableAdapter.Update` 方法还用于通过将 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> 或 <xref:System.Data.DataRow> 的数组作为方法参数，将数据集中的更改协调回数据库。|
|`TableAdapter.Delete`|基于作为方法参数传入的原始列值，从数据库中删除现有记录。|

## <a name="to-save-new-records-from-an-object-to-a-database"></a>将新记录从对象保存到数据库

- 通过向 `TableAdapter.Insert` 方法传递值来创建记录。

     以下示例通过向 `TableAdapter.Insert` 方法传递 `currentCustomer` 对象中的值，在 `Customers` 表中创建新的客户记录。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet23":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet23":::

## <a name="to-update-existing-records-from-an-object-to-a-database"></a>将现有记录从对象更新到数据库

- 通过调用 `TableAdapter.Update` 方法、传入新值以更新记录并传入原始值以查找记录，从而修改记录。

    > [!NOTE]
    > 对象需要保留原始值，以便将它们传递给 `Update` 方法。 此示例使用前缀为 `orig` 的属性来存储原始值。

     以下示例通过向 `TableAdapter.Update` 方法传递 `Customer` 对象中的新值和原始值来更新 `Customers` 表中的现有记录。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet24":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet24":::

## <a name="to-delete-existing-records-from-a-database"></a>删除数据库中的现有记录

- 通过调用 `TableAdapter.Delete` 方法并传入原始值来查找记录，从而删除记录。

    > [!NOTE]
    > 对象需要保留原始值，以便将它们传递给 `Delete` 方法。 此示例使用前缀为 `orig` 的属性来存储原始值。

     以下示例通过向 `TableAdapter.Delete` 方法传递 `Customer` 对象中的原始值，从 `Customers` 表中删除记录。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet25":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet25":::

## <a name="net-security"></a>.NET 安全性

必须有权对数据库中的表执行选定的 `INSERT`、`UPDATE` 或 `DELETE`。

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
