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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122154857"
---
# <a name="query-datasets"></a>查询数据集
若要搜索数据集中的特定记录，请使用 DataTable 上的 方法，编写自己的 foreach 语句以循环访问表的 Rows 集合，或使用 LINQ to DataSet `FindBy` 。 [](/dotnet/framework/data/adonet/linq-to-dataset)

## <a name="dataset-case-sensitivity"></a>数据集区分大小写
在数据集中，表名和列名默认不区分大小写 - 也就是说，名为"Customers"的数据集中的表也可以称为"customers"。 这匹配许多数据库中的命名约定，包括SQL Server。 在这种情况下SQL Server，默认行为是不能仅按大小写区分数据元素的名称。

> [!NOTE]
> 与数据集不同，XML 文档区分大小写，因此架构中定义的数据元素的名称区分大小写。 例如，架构协议允许架构定义名为"Customers"的表和名为"customers"的不同表。 当包含仅大小写不同的元素的架构用于生成数据集类时，这可能会导致名称冲突。

但是，区分大小写可能是数据集中数据解释方式的一个因素。 例如，如果筛选数据集表中的数据，则搜索条件可能会返回不同的结果，具体取决于比较是否区分大小写。 可以通过设置数据集的 属性来控制筛选、搜索和排序的区分 <xref:System.Data.DataSet.CaseSensitive%2A> 大小写。 默认情况下，数据集中所有表都继承此属性的值。  (可以通过设置表的 property.) 来覆盖每个表 <xref:System.Data.DataTable.CaseSensitive%2A> 的此属性

## <a name="locate-a-specific-row-in-a-data-table"></a>在数据表中查找特定行

#### <a name="to-find-a-row-in-a-typed-dataset-with-a-primary-key-value"></a>查找类型数据集中具有主键值的行

- 若要查找行，请调用使用表的主键的强 `FindBy` 类型方法。

     在下面的示例中， `CustomerID` 列是表的主 `Customers` 键。 这意味着生成的方法是 `FindBy` `FindByCustomerID` 。 该示例演示如何使用生成的 <xref:System.Data.DataRow> 方法将特定的 分配给 `FindBy` 变量。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet18":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet18":::

#### <a name="to-find-a-row-in-an-untyped-dataset-with-a-primary-key-value"></a>在非类型化数据集中查找具有主键值的行

- 调用 <xref:System.Data.DataRowCollection.Find%2A> 集合的 <xref:System.Data.DataRowCollection> 方法，将主键作为参数传递。

     下面的示例演示如何声明名为 的新行 `foundRow` ，并为其分配 方法的返回 <xref:System.Data.DataRowCollection.Find%2A> 值。 如果找到主键，则列索引 1 的内容将显示在消息框中。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet19":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet19":::

## <a name="find-rows-by-column-values"></a>按列值查找行

#### <a name="to-find-rows-based-on-the-values-in-any-column"></a>根据任何列中的值查找行

- 数据表是使用 方法创建的，该方法基于传递给 方法的表达式 <xref:System.Data.DataTable.Select%2A> <xref:System.Data.DataRow> 返回 的 <xref:System.Data.DataTable.Select%2A> 数组。 有关创建有效表达式的信息，请参阅有关 属性的页面的"表达式语法" <xref:System.Data.DataColumn.Expression%2A> 部分。

     下面的示例演示如何使用 的 <xref:System.Data.DataTable.Select%2A> 方法 <xref:System.Data.DataTable> 查找特定行。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet20":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet20":::

## <a name="access-related-records"></a>访问相关记录
当数据集中的表相关时， <xref:System.Data.DataRelation> 对象可以使相关记录在另一个表中可用。 例如，可以使用包含 和 `Customers` `Orders` 表的数据集。

可以通过在父表中调用 的 方法，使用 对象 <xref:System.Data.DataRelation> <xref:System.Data.DataRow.GetChildRows%2A> <xref:System.Data.DataRow> 查找相关记录。 此方法返回相关子记录的数组。 或者，可以在 <xref:System.Data.DataRow.GetParentRow%2A> 子表中调用 的 <xref:System.Data.DataRow> 方法。 此方法从父表中 <xref:System.Data.DataRow> 返回单个 。

本页提供了使用类型数据集的示例。 有关在非类型化数据集中导航关系的信息，请参阅 [导航 DataRelations](/dotnet/framework/data/adonet/dataset-datatable-dataview/navigating-datarelations)。

> [!NOTE]
> 如果使用的是 Windows 窗体应用程序，并且使用数据绑定功能来显示数据，设计器生成的窗体可能会为应用程序提供足够的功能。 有关详细信息，请参阅[将控件绑定到](../data-tools/bind-controls-to-data-in-visual-studio.md)Visual Studio。 具体而言，请参阅 [数据集中的关系](relationships-in-datasets.md)。

下面的代码示例演示如何在类型数据集中向上和向下导航关系。 这些代码示例使用类型 () <xref:System.Data.DataRow> `NorthwindDataSet.OrdersRow` 生成的 FindBy *PrimaryKey* () 方法查找所需的行并返回 `FindByCustomerID` 相关记录。 这些示例仅在你具有以下功能时正确编译和运行：

- 具有表的名为 `NorthwindDataSet` 的数据集 `Customers` 的实例。

- 表 `Orders` 。

- 名为 的关系 `FK_Orders_Customers` ，该关系与两个表相关。

此外，需要用数据填充这两个表，以返回任何记录。

#### <a name="to-return-the-child-records-of-a-selected-parent-record"></a>返回所选父记录的子记录

- 调用 <xref:System.Data.DataRow.GetChildRows%2A> 特定数据行的 `Customers` 方法，并返回表中的行 `Orders` 数组：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet6":::

#### <a name="to-return-the-parent-record-of-a-selected-child-record"></a>返回所选子记录的父记录

- 调用 <xref:System.Data.DataRow.GetParentRow%2A> 特定数据行的 `Orders` 方法，并返回表中的单个 `Customers` 行：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDatasets/CS/Form1.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDatasets/VB/Form1.vb" id="Snippet7":::

## <a name="see-also"></a>请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
