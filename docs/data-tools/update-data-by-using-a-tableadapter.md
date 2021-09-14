---
title: 使用 TableAdapter 更新数据
description: 更新数据集中的数据。 通过调用 TableAdapter 的 Update 方法将数据发送回数据库。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 38f804232dd633be82e328716312c9c8f1cf53e6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601069"
---
# <a name="update-data-by-using-a-tableadapter"></a>使用 TableAdapter 更新数据

修改并验证数据集中的数据后，可以通过调用 `Update` [TableAdapter](../data-tools/create-and-configure-tableadapters.md)的 方法将更新后的数据发送回数据库。 方法 `Update` 更新单个数据表， (表中每个数据行的) INSERT、UPDATE 或 DELETE 数据库运行 <xref:System.Data.DataRow.RowState%2A> 正确的命令。 数据集具有相关表时，Visual Studio生成用于执行更新的 TableAdapterManager 类。 TableAdapterManager 类可确保根据数据库中定义的外键约束以正确的顺序进行更新。 使用数据绑定控件时，数据绑定体系结构会创建名为 tableAdapterManager 的 TableAdapterManager 类的成员变量。

> [!NOTE]
> 尝试使用数据集的内容更新数据源时，可能会出现错误。 为了避免错误，建议将调用适配器方法的代码放在 `Update` 块 `try` / `catch` 中。

更新数据源的确切过程可能因业务需求而异，但包括以下步骤：

1. 在 块中 `Update` 调用适配器的 `try` / `catch` 方法。

2. 如果捕获到异常，请找到导致错误的数据行。

3. 如果可以，请以编程 (方式协调数据行中的问题，或者向用户显示无效行以修改) ，然后再次尝试 (<xref:System.Data.DataRow.HasErrors%2A> <xref:System.Data.DataTable.GetErrors%2A> 、) 。

## <a name="save-data-to-a-database"></a>将数据保存到数据库

调用 `Update` TableAdapter 的 方法。 传递包含要写入数据库的值的数据表的名称。

### <a name="to-update-a-database-by-using-a-tableadapter"></a>使用 TableAdapter 更新数据库

- 将 TableAdapter 的 `Update` 方法括在 `try` / `catch` 块中。 下面的示例演示如何从 块中更新 中的 `Customers` `NorthwindDataSet` 表 `try` / `catch` 的内容。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet9":::

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
