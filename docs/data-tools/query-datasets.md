---
title: 查询数据集
description: 了解查询数据集。 了解数据集区分大小写。 在数据表中查找特定行、按列值查找行以及访问相关记录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
ms.assetid: 7b1a91cf-8b5a-4fc0-ac36-0dc2d336fa1b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 2f047f38327f0773f7b370ba721b7e88afed2b90
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601114"
---
# <a name="query-datasets"></a>查询数据集
若要搜索数据集中的特定记录，请使用 DataTable 上的 `FindBy` 方法，编写自己的 foreach 语句以循环访问表的行集合，或使用 [LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset)。

## <a name="dataset-case-sensitivity"></a>数据集区分大小写
在数据集中，表名和列名默认不区分大小写；也就是说，数据集中名为“Customers”的表也可以称为“customers”。 这与许多数据库（包括 SQL Server）中的命名约定一致。 在 SQL Server 中，默认行为是不能仅按大小写区分数据元素的名称。

> [!NOTE]
> 与数据集不同，XML 文档区分大小写，因此架构中定义的数据元素的名称区分大小写。 例如，架构协议允许架构定义一个名为“Customers”的表和一个名为“customers”的不同的表。 使用的架构包含仅有大小写不同的元素，用于生成数据集类时可能会导致名称冲突。

但是，区分大小写可能是数据集中数据解释方式的一个因素。 例如，如果你筛选数据集表中的数据，搜索条件可能会返回不同的结果，具体取决于比较是否区分大小写。 可以通过设置数据集的 <xref:System.Data.DataSet.CaseSensitive%2A> 属性来控制筛选、搜索和排序是否区分大小写。 默认情况下，数据集中所有表都继承此属性的值。 （可以通过设置表的 <xref:System.Data.DataTable.CaseSensitive%2A> 属性来覆盖每个表的此项属性。）

## <a name="locate-a-specific-row-in-a-data-table"></a>在数据表中查找特定行

#### <a name="to-find-a-row-in-a-typed-dataset-with-a-primary-key-value"></a>查找类型化数据集中具有主键值的行

- 若要查找行，请调用使用表的主键的强类型 `FindBy` 方法。

     在下面的示例中，`CustomerID` 列是 `Customers` 表的主键。 这意味着生成的 `FindBy` 方法是 `FindByCustomerID`。 该示例演示如何使用生成的 `FindBy` 方法将特定的 <xref:System.Data.DataRow> 分配给变量。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet18":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet18":::

#### <a name="to-find-a-row-in-an-untyped-dataset-with-a-primary-key-value"></a>查找非类型化数据集中具有主键值的行

- 调用 <xref:System.Data.DataRowCollection> 集合的 <xref:System.Data.DataRowCollection.Find%2A> 方法，同时将主键作为参数传递。

     下面的示例演示如何声明名为 `foundRow` 的新行，并为其分配 <xref:System.Data.DataRowCollection.Find%2A> 方法的返回值。 如果找到主键，则列索引 1 的内容将显示在消息框中。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet19":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet19":::

## <a name="find-rows-by-column-values"></a>按列值查找行

#### <a name="to-find-rows-based-on-the-values-in-any-column"></a>根据任何列中的值查找行

- 数据表是使用 <xref:System.Data.DataTable.Select%2A> 方法创建的，<xref:System.Data.DataRow> 方法根据传递给该方法的表达式返回一个 <xref:System.Data.DataTable.Select%2A> 数组。 有关创建有效表达式的详细信息，请参阅有关 <xref:System.Data.DataColumn.Expression%2A> 属性的页面的“表达式语法”部分。

     以下示例演示了如何使用 <xref:System.Data.DataTable> 的 <xref:System.Data.DataTable.Select%2A> 方法来查找特定行。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet20":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet20":::

## <a name="access-related-records"></a>访问相关记录
当数据集中的表相关时，<xref:System.Data.DataRelation> 对象可以使相关记录在另一个表中可用。 例如，包含 `Customers` 和 `Orders` 表的数据集可供使用。

通过在父表中调用 <xref:System.Data.DataRow> 的 <xref:System.Data.DataRow.GetChildRows%2A> 方法，你可以使用 <xref:System.Data.DataRelation> 对象查找相关记录。 此方法返回一个相关子记录的数组。 或者，可以在子表中调用 <xref:System.Data.DataRow> 的 <xref:System.Data.DataRow.GetParentRow%2A> 方法。 此方法从父表中返回单个 <xref:System.Data.DataRow>。

本页提供了使用类型化数据集的示例。 有关非类型化数据集中导航关系的信息，请参阅[导航 DataRelation](/dotnet/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations)。

> [!NOTE]
> 如果你使用的是 Windows 窗体应用程序，并且使用数据绑定功能来显示数据，设计器生成的窗体可能会为应用程序提供足够的功能。 有关详细信息，请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。 具体请参阅[数据集中的关系](relationships-in-datasets.md)。

下面的代码示例演示如何在类型化数据集中向上和向下导航关系。 代码示例使用类型化 <xref:System.Data.DataRow> (`NorthwindDataSet.OrdersRow`) 和生成的 FindBy PrimaryKey (`FindByCustomerID`) 方法来查找所需的行并返回相关记录。 这些示例仅在你拥有以下项时才能正确编译和运行：

- 包含 `Customers` 表的名为 `NorthwindDataSet` 的数据集的实例。

- `Orders` 表。

- 将这两个表关联起来的名为 `FK_Orders_Customers` 的关系。

此外，需要用数据填充这两个表，以返回任何记录。

#### <a name="to-return-the-child-records-of-a-selected-parent-record"></a>返回所选父记录的子记录

- 调用特定 `Customers` 数据行的 <xref:System.Data.DataRow.GetChildRows%2A> 方法，从 `Orders` 表中返回行的数组：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet6":::

#### <a name="to-return-the-parent-record-of-a-selected-child-record"></a>返回所选子记录的父记录

- 调用特定 `Orders` 数据行的 <xref:System.Data.DataRow.GetParentRow%2A> 方法，从 `Customers` 表中返回单行：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet7":::

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
