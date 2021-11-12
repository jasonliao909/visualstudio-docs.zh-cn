---
title: 创建参数化 TableAdapter 查询
description: 了解如何创建参数化 TableAdapter 查询。 参数化查询将返回满足查询内的 WHERE 子句条件的数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- TableAdapters, parameterized queries
- data [Visual Studio], searching data
- queries [Visual Studio], creating
- TableAdapters, searching data
- queries [Visual Studio], TableAdapters
ms.assetid: 104d1d19-b5a9-4071-b81e-1b3af08e9c7b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 53ede3f31574ec2bbbd9b5cc2ce1f588b4ed5233
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601182"
---
# <a name="create-parameterized-tableadapter-queries"></a>创建参数化 TableAdapter 查询

参数化查询将返回满足查询内的 WHERE 子句条件的数据。 例如，通过在返回客户列表的 SQL 语句的末尾添加 `WHERE City = @City`，可以参数化客户列表，使之只显示某个城市的客户。

可在“数据集设计器”中创建参数化 TableAdapter 查询，也可使用“数据”菜单上的“参数化数据源”命令在 Windows 应用程序中创建此类查询  。 “参数化数据源”命令会在窗体上创建控件，用于输入参数值和运行查询。

> [!NOTE]
> 构造参数化查询时，使用特定于要编码的数据库的参数表示法。 例如，Access 和 OleDb 数据源使用问号“?”表示参数，所以 WHERE 子句将类似于：`WHERE City = ?`。

## <a name="create-a-parameterized-tableadapter-query"></a>创建参数化 TableAdapter 查询

### <a name="to-create-a-parameterized-query-in-the-dataset-designer"></a>在“数据集设计器”中创建参数化查询

- 将 WHERE 子句和所需参数添加到 SQL 语句中，以创建新的 TableAdapter。 有关详细信息，请参阅[创建和配置 TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

     -或-

- 将 WHERE 子句和所需参数添加到 SQL 语句中，以向现有 TableAdapter 中添加查询。

### <a name="to-create-a-parameterized-query-while-designing-a-data-bound-form"></a>在设计数据绑定窗体时创建参数化查询

1. 在窗体中选择已绑定到数据集的控件。 有关详细信息，请参阅[在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)。

2. 在“数据”菜单上，选择“添加查询” 。

3. 将 WHERE 语句和所需参数添加到 SQL 语句中，以完成“搜索标准生成器”对话框。

### <a name="to-add-a-query-to-an-existing-data-bound-form"></a>将查询添加到现有数据绑定窗体

1. 在“Windows 窗体设计器”中打开窗体。

2. 在“数据”菜单上，选择“添加查询”或“数据智能标记”  。

    > [!NOTE]
    > 如果“添加查询”在“数据”菜单上不可用，请在窗体上选择一个控件，该窗体将显示你希望参数化功能添加到的数据源。 例如，如果窗体在 <xref:System.Windows.Forms.DataGridView> 控件中显示数据，则选择该控件。 如果窗体在各个控件中显示数据，则选择任意数据绑定控件。

3. 在“选择数据源表”区域中，选择要添加参数化的表。

4. 如果要创建新查询，请在“新建查询名称”框中键入名称。

     -或-

     在“现有查询名称”框中选择查询。

5. 在“查询文本”框中，键入一个采用参数的查询。

6. 选择“确定”。

     用于输入参数的控件和“加载”按钮将添加到 <xref:System.Windows.Forms.ToolStrip> 控件的窗体中。

### <a name="query-for-null-values"></a>查询 NULL 值

如果要查询不包含当前值的记录，则可以为 TableAdapter 参数赋予空值。 例如，假设以下查询的 `WHERE` 子句中有一个 `ShippedDate` 参数：

```sql
SELECT CustomerID, OrderDate, ShippedDate
FROM Orders
WHERE (ShippedDate = @ShippedDate) OR (ShippedDate IS NULL)
```

如果这是针对 TableAdapter 的查询，可以使用以下代码查询所有未发货的订单：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Form2.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Form2.vb" id="Snippet8":::

若要使查询能够接受 NULL 值，请执行以下操作：

1. 在“数据集设计器”中，选择需要接受 NULL 参数值的 TableAdapter 查询。

2. 在“属性”窗口中，选择“参数”，然后单击省略号 (…) 按钮，打开“参数集合编辑器”   。

3. 选择允许存在 NULL 值的参数并将 AllowDbNull 属性设置为 `true`。

## <a name="see-also"></a>另请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
