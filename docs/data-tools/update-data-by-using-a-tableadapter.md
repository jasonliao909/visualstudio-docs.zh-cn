---
title: 使用 TableAdapter 更新数据
description: 更新数据集中的数据。 通过调用 TableAdapter 的 Update 方法，可将数据发送回数据库。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601069"
---
# <a name="update-data-by-using-a-tableadapter"></a>使用 TableAdapter 更新数据

在修改并验证数据集中的数据之后，可通过调用 [TableAdapter](../data-tools/create-and-configure-tableadapters.md) 的 `Update` 方法将更新后的数据发送回数据库。 `Update` 方法更新单个数据表，并基于表中每个数据行的 <xref:System.Data.DataRow.RowState%2A> 运行正确的命令（INSERT、UPDATE 或 DELETE）。 如果数据集具有相关表，Visual Studio 会生成一个 TableAdapterManager 类，用于执行更新。 TableAdapterManager 类可确保根据数据库中定义的外键约束以正确的顺序进行更新。 如果使用数据绑定控件，数据绑定体系结构会创建 TableAdapterManager 类的成员变量（名为 tableAdapterManager）。

> [!NOTE]
> 如果尝试使用数据集的内容更新数据源，可能会收到错误。 为了避免错误，建议将用于调用适配器 `Update` 方法的代码放在 `try`/`catch` 块中。

具体的数据源更新过程可能因业务需求而异，但包括以下步骤:

1. 调用 `try`/`catch` 块中适配器的 `Update` 方法。

2. 如果捕获到异常，请找到导致该错误的数据行。

3. 协调数据行中的问题（如果可以，可通过编程方式，也可向用户显示无效的行以让其修改），然后再次尝试更新（<xref:System.Data.DataRow.HasErrors%2A>、<xref:System.Data.DataTable.GetErrors%2A>）。

## <a name="save-data-to-a-database"></a>将数据保存到数据库

调用 TableAdapter 的 `Update` 方法。 传递数据表（包含要写入数据库的值）的名称。

### <a name="to-update-a-database-by-using-a-tableadapter"></a>使用 TableAdapter 更新数据库

- 将 TableAdapter 的 `Update` 方法放入 `try`/`catch` 块中。 以下示例演示如何从 `try`/`catch` 块中更新 `NorthwindDataSet` 中 `Customers` 表的内容。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet9":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet9":::

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
