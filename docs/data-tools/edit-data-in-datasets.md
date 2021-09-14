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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601164"
---
# <a name="edit-data-in-datasets"></a>编辑数据集中的数据
编辑数据表中的数据与编辑任何数据库中的表中的数据非常类似。 该过程可能包括插入、更新和删除表中的记录。 在数据绑定窗体中，可以指定用户可编辑的字段。 在这种情况下，数据绑定基础结构会处理所有更改跟踪，以便以后可以将更改发送回数据库。 如果以编程方式对数据进行编辑，并且打算将这些更改发送回数据库，则必须使用执行更改跟踪的对象和方法。

除了更改实际数据之外，还可以查询 <xref:System.Data.DataTable> 以返回特定数据行。 例如，可以查询单个行、原始 (建议行、) 更改的行或具有错误的行。

## <a name="to-edit-rows-in-a-dataset"></a>编辑数据集中的行
若要编辑 中的现有行，需要找到要编辑的 ，然后将更新的值 <xref:System.Data.DataTable> <xref:System.Data.DataRow> 分配给所需的列。

如果不知道要编辑的行的索引，请使用 方法 `FindBy` 按主键进行搜索：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet3":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet3":::

如果知道行索引，可以按如下所示访问和编辑行：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet5":::

## <a name="to-insert-new-rows-into-a-dataset"></a>将新行插入数据集
使用数据绑定控件的应用程序通常通过[BindingNavigator](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)控件上的"添加新"按钮添加新记录。

若要手动将新记录添加到数据集，请通过调用 DataTable 上的 方法创建新的数据行。 然后，将行添加到 <xref:System.Data.DataRow> 集合 () <xref:System.Data.DataTable.Rows%2A> 的 行 <xref:System.Data.DataTable> ：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet1":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet1":::

若要保留数据集向数据源发送更新所需的信息，请使用 方法 <xref:System.Data.DataRow.Delete%2A> 删除数据表中的行。 例如，如果应用程序使用 TableAdapter (或 <xref:System.Data.Common.DataAdapter>) ，则 TableAdapter 的 方法将删除 数据库中 具有 的 `Update` <xref:System.Data.DataRow.RowState%2A> 行 <xref:System.Data.DataRowState.Deleted> 。

如果应用程序不需要将更新发送回数据源，则通过直接访问数据行集合来删除记录 <xref:System.Data.DataRowCollection.Remove%2A> () 。

#### <a name="to-delete-records-from-a-data-table"></a>从数据表中删除记录

- 调用 <xref:System.Data.DataRow.Delete%2A> 的 方法 <xref:System.Data.DataRow> 。

     此方法不会以物理方式删除记录。 而是标记要删除的记录。

    > [!NOTE]
    > 如果获取 的 count 属性 <xref:System.Data.DataRowCollection> ，则生成的计数包括已标记为要删除的记录。 若要获取未标记为要删除的记录的准确计数，可以循环访问集合，查看每个记录的 <xref:System.Data.DataRow.RowState%2A> 属性。  (标记为要删除的记录的 为 .) 或者，你可以创建数据集的数据视图，该数据集基于行状态进行筛选，然后从该视图 <xref:System.Data.DataRow.RowState%2A> <xref:System.Data.DataRowState.Deleted> 获取 count 属性。

以下示例演示如何调用 方法 <xref:System.Data.DataRow.Delete%2A> ，将表中的第一行 `Customers` 标记为已删除：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet8":::

## <a name="determine-if-there-are-changed-rows"></a>确定是否有更改的行
对数据集中的记录进行更改时，将存储有关这些更改的信息，直到提交这些更改。 在调用数据集或数据表的 方法时，或在调用 `AcceptChanges` TableAdapter 或数据适配器的 方法时提交 `Update` 更改。

在每个数据行中，通过两种方式跟踪更改：

- 每个数据行都包含与数据行 (， <xref:System.Data.DataRow.RowState%2A> 例如 <xref:System.Data.DataRowState.Added> 、、 或 <xref:System.Data.DataRowState.Modified> <xref:System.Data.DataRowState.Deleted> <xref:System.Data.DataRowState.Unchanged>) 。

- 每个更改后的数据行都包含该行 () 版本、 (更改前 (版本) 更改后 (版本 <xref:System.Data.DataRowVersion>) 。 在更改挂起期间 (响应事件) ，第三个版本（建议的版本） <xref:System.Data.DataTable.RowChanging> 也可用。

如果在 <xref:System.Data.DataSet.HasChanges%2A> 数据集中进行了 `true` 更改，则数据集的 方法返回 。 确定更改的行存在后，可以调用 或 的 方法 `GetChanges` <xref:System.Data.DataSet> <xref:System.Data.DataTable> 以返回一组已更改的行。

#### <a name="to-determine-if-changes-have-been-made-to-any-rows"></a>确定是否对任意行进行了更改

- 调用 <xref:System.Data.DataSet.HasChanges%2A> 数据集的 方法以检查更改的行。

下面的示例演示如何检查 方法的返回值，以检测名为 的数据集 <xref:System.Data.DataSet.HasChanges%2A> 中是否有更改的行 `NorthwindDataset1` ：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet12":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet12":::

## <a name="determine-the-type-of-changes"></a>确定更改的类型
还可以检查数据集中进行了哪些类型的更改，方法是将枚举中的值 <xref:System.Data.DataRowState> 传递给 <xref:System.Data.DataSet.HasChanges%2A> 方法。

#### <a name="to-determine-what-type-of-changes-have-been-made-to-a-row"></a>确定对行进行了哪些类型的更改

- 将 <xref:System.Data.DataRowState> 值传递给 <xref:System.Data.DataSet.HasChanges%2A> 方法。

以下示例演示如何检查名为 的数据集 `NorthwindDataset1` ，以确定是否向该数据集添加了任何新行：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet13":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet13":::

## <a name="to-locate-rows-that-have-errors"></a>查找有错误的行
使用单个列和数据行时，可能会遇到错误。 可以检查 `HasErrors` 属性，以确定 、 或 <xref:System.Data.DataSet> 中 <xref:System.Data.DataTable> 是否存在错误 <xref:System.Data.DataRow> 。

1. 检查 `HasErrors` 属性，查看数据集中是否有错误。

2. 如果 属性为 ，则会浏览表的集合，然后通过行来查找 `HasErrors` `true` 出现错误的行。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet23":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet23":::

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
