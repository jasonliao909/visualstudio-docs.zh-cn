---
title: 将数据从对象保存到数据库
description: 使用数据集中的 DataSet 工具将数据从对象保存到Visual Studio。 了解如何保存新记录、更新现有记录以及删除现有记录。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122059198"
---
# <a name="save-data-from-an-object-to-a-database"></a>将数据从对象保存到数据库

可以通过将对象中的值传递到 TableAdapter 的 DBDirect 方法之一（例如， (，将数据保存到 `TableAdapter.Insert`) 。 有关详细信息，请参阅 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

若要从 对象集合保存数据，请循环访问对象集合 (例如 for-next 循环) ，然后使用 TableAdapter 的某个方法将每个对象的值发送到 `DBDirect` 数据库。

默认情况下， `DBDirect` 方法是在可直接针对数据库运行的 TableAdapter 上创建的。 可以直接调用这些方法，并且不需要 或 对象来协调更改， <xref:System.Data.DataSet> <xref:System.Data.DataTable> 以便向数据库发送更新。

> [!NOTE]
> 配置 TableAdapter 时，主查询必须提供足够的信息，以便 `DBDirect` 创建方法。 例如，如果将 TableAdapter 配置为从未定义主键列的表中查询数据，则它不会生成 `DBDirect` 方法。

|TableAdapter DBDirect 方法|说明|
| - |-----------------|
|`TableAdapter.Insert`|将新记录添加到数据库，使你能够将单个列值作为方法参数传递。|
|`TableAdapter.Update`|更新数据库中的现有记录。 方法 `Update` 采用原始列值和新列值作为方法参数。 原始值用于查找原始记录，新值用于更新该记录。<br /><br /> 方法还用于将 、 、 或 的数组作为方法参数，将数据集中的更改协调 `TableAdapter.Update` <xref:System.Data.DataSet> <xref:System.Data.DataTable> <xref:System.Data.DataRow> <xref:System.Data.DataRow> 回数据库。|
|`TableAdapter.Delete`|基于作为方法参数传入的原始列值，从数据库中删除现有记录。|

## <a name="to-save-new-records-from-an-object-to-a-database"></a>将新记录从对象保存到数据库

- 通过向 方法传递值来创建 `TableAdapter.Insert` 记录。

     下面的示例通过向 方法传递 对象中的值，在 表中 `Customers` `currentCustomer` 创建新的客户 `TableAdapter.Insert` 记录。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet23":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet23":::

## <a name="to-update-existing-records-from-an-object-to-a-database"></a>将现有记录从 对象更新到数据库

- 通过调用 方法修改记录，传递新值以更新记录，并传递原始值 `TableAdapter.Update` 以查找记录。

    > [!NOTE]
    > 对象需要保留原始值，以便将它们传递给 `Update` 方法。 此示例使用前缀为 `orig` 的属性来存储原始值。

     以下示例通过向 方法传递 对象中的新值和原始值来更新 `Customers` `Customer` 表中的现有 `TableAdapter.Update` 记录。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet24":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet24":::

## <a name="to-delete-existing-records-from-a-database"></a>从数据库中删除现有记录

- 通过调用 方法并传递原始值来查找 `TableAdapter.Delete` 记录，删除记录。

    > [!NOTE]
    > 对象需要保留原始值，以便将它们传递给 `Delete` 方法。 此示例使用前缀为 `orig` 的属性来存储原始值。

     以下示例通过向 方法传递 对象中的原始值，从 表 `Customers` `Customer` 中删除 `TableAdapter.Delete` 记录。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet25":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet25":::

## <a name="net-security"></a>.NET 安全性

您必须有权对数据库中的表执行选定的 、 `INSERT` `UPDATE` 或 `DELETE` 。

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
