---
title: 编辑数据集中的数据
description: 了解如何编辑数据集中的数据。 了解如何编辑数据集行、将新行插入数据集、确定是否有更改的行以及查找具有错误的行。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- datasets [Visual Basic], editing data
- data [Visual Studio], editing in datasets
ms.assetid: 50d5c580-fbf7-408f-be70-e63ac4f4d0eb
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 5cec6bccd2f1b2e6dd2e8250039a82cb4607b65d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601164"
---
# <a name="edit-data-in-datasets"></a>编辑数据集中的数据
编辑数据表中的数据与编辑任何数据库中的表中的数据非常类似。 该过程可能包括插入、更新和删除表中的记录。 在数据绑定窗体中，可以指定用户可编辑的字段。 在这种情况下，数据绑定基础结构会处理所有更改跟踪，以便以后可以将更改发送回数据库。 如果以编程方式对数据进行编辑，并且打算将这些更改发送回数据库，则必须使用用于执行更改跟踪的对象和方法。

除更改实际数据之外，还可查询 <xref:System.Data.DataTable> 以返回特定数据行。 例如，可查询单个行、特定版本的行（原始和建议）、更改的行或具有错误的行。

## <a name="to-edit-rows-in-a-dataset"></a>编辑数据集中的行
若要编辑 <xref:System.Data.DataTable> 中的现有行，需要找到要编辑的 <xref:System.Data.DataRow>，然后将更新的值分配给所需的列。

如果不知道要编辑的行的索引，请使用 `FindBy` 方法按主键进行搜索：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet3":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet3":::

如果知道行索引，可按如下所示访问和编辑行：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet5":::

## <a name="to-insert-new-rows-into-a-dataset"></a>将新行插入数据集
使用数据绑定控件的应用程序通常通过 [BindingNavigator 控件](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)上的“添加新项”按钮来添加新记录。

若要将新记录手动添加到数据集，请通过调用 DataTable 上的方法创建新的数据行。 然后，将该行添加到 <xref:System.Data.DataTable> 的 <xref:System.Data.DataRow> 集合 (<xref:System.Data.DataTable.Rows%2A>)：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet1":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet1":::

若要保留数据集向数据源发送更新所需的信息，请使用 <xref:System.Data.DataRow.Delete%2A> 方法删除数据表中的行。 例如，如果应用程序使用 TableAdapter（或 <xref:System.Data.Common.DataAdapter>），则 TableAdapter 的 `Update` 方法会删除数据库中具有 <xref:System.Data.DataRowState.Deleted> 的 <xref:System.Data.DataRow.RowState%2A> 的行。

如果应用程序不需要将更新发送回数据源，则可通过直接访问数据行集合 (<xref:System.Data.DataRowCollection.Remove%2A>) 来删除记录。

#### <a name="to-delete-records-from-a-data-table"></a>删除记录集中的记录

- 调用 <xref:System.Data.DataRow> 的 <xref:System.Data.DataRow.Delete%2A> 方法。

     此方法不会以物理方式删除记录。 而是标记要删除的记录。

    > [!NOTE]
    > 如果获取 <xref:System.Data.DataRowCollection> 的 count 属性，则生成的计数包括已标记为要删除的记录。 若要获取未标记为要删除的记录的准确计数，可以循环访问集合，查看每条记录的 <xref:System.Data.DataRow.RowState%2A> 属性。 （标记为删除的记录具有 <xref:System.Data.DataRowState.Deleted> 的 <xref:System.Data.DataRow.RowState%2A>。）或者，可以创建数据集的数据视图，该数据集基于行状态进行筛选，然后从该视图获取 count 属性。

以下示例演示如何调用 <xref:System.Data.DataRow.Delete%2A> 方法，以将 `Customers` 表中的第一行标记为已删除：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet8":::

## <a name="determine-if-there-are-changed-rows"></a>确定是否有更改的行
对数据集中的记录进行更改时，将存储有关这些更改的信息，直到提交这些更改。 在调用数据集或数据表的 `AcceptChanges` 方法时，或在调用 TableAdapter 或数据适配器的 `Update` 方法时提交更改。

在每个数据行中，通过以下两种方式跟踪更改：

- 每个数据行都包含与其 <xref:System.Data.DataRow.RowState%2A> 相关的信息（例如 <xref:System.Data.DataRowState.Added>、<xref:System.Data.DataRowState.Modified>、<xref:System.Data.DataRowState.Deleted> 或 <xref:System.Data.DataRowState.Unchanged>）。

- 每个更改后的数据行都包含该行 (<xref:System.Data.DataRowVersion>) 的多个版本、原始版本（更改之前）和当前版本（更改之后）。 在更改挂起期间（可以响应 <xref:System.Data.DataTable.RowChanging> 事件的时候），第三个版本（建议的版本）也可用。

如果在数据集中进行了更改，则数据集的 <xref:System.Data.DataSet.HasChanges%2A> 方法将返回 `true`。 确定已更改的行存在后，可调用 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 的 `GetChanges` 方法来返回一组已更改的行。

#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>确定是否对任意行进行了更改

- 调用数据集的 <xref:System.Data.DataSet.HasChanges%2A> 方法以检查是否有更改的行。

以下示例演示如何检查 <xref:System.Data.DataSet.HasChanges%2A> 方法的返回值，以检测名为 `NorthwindDataset1` 的数据集中是否有更改的行：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet12":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet12":::

## <a name="determine-the-type-of-changes"></a>确定更改的类型
还可检查数据集中进行了哪些类型的更改，方法是将 <xref:System.Data.DataRowState> 枚举中的值传递给 <xref:System.Data.DataSet.HasChanges%2A> 方法。

#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>确定对行进行了哪些类型的更改

- 向 <xref:System.Data.DataSet.HasChanges%2A> 方法传递 <xref:System.Data.DataRowState> 值。

以下示例演示如何检查名为 `NorthwindDataset1` 的数据集，以确定是否向该数据集添加了任何新行：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet13":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet13":::

## <a name="to-locate-rows-that-have-errors"></a>查找出错的行
使用单个列和数据行时，可能会遇到错误。 可检查 `HasErrors` 属性来确定 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> 中是否存在错误。

1. 检查 `HasErrors` 属性，查看数据集中是否有错误。

2. 如果 `HasErrors` 属性为 `true`，则循环访问表的集合，然后通过行来查找出现错误的行。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet23":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet23":::

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
