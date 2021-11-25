---
title: 验证数据集中的数据
description: 学习验证数据集中的数据。 验证数据涉及到确认输入到数据对象中的值符合数据集架构内的约束。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- DataTable.ColumnChanging
- System.Data.DataTable.ColumnChanging
- System.Data.DataTable.RowChanging
- DataTable.RowChanging
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data validation, datasets
- data validation
- validating data, datasets
- updating datasets, validating data
ms.assetid: 79500596-1e4d-478e-a991-a636fd73a622
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 8c018ea86dc3bd3c2bcd5f676c7ef33b17cbb217
ms.sourcegitcommit: 8671132ee0425b273b060fa35c75657e7ae02583
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2021
ms.locfileid: "132924272"
---
# <a name="validate-data-in-datasets"></a>验证数据集中的数据
验证数据是确认输入到数据对象中的值符合数据集架构内的约束的过程。 验证过程还会确认这些值遵循已为应用程序建立的规则。 在将更新发送到基础数据库之前对数据进行验证是一种很好的做法。 这可以减少错误，还能减少应用程序和数据库之间的潜在往返行程次数。

可以通过在数据集本身中构建验证检查，来确认写入数据集的数据是有效的。 无论如何执行更新（无论是通过表单中的控件直接更新、在组件中更新，还是通过其他方式更新），数据集都可以检测数据。 由于数据集是应用程序的一部分（与数据库后端不同），因此在其中构建特定于应用程序的验证是符合逻辑的。

向应用程序添加验证的最佳位置是数据集的分部类文件中。 在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 或 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 中打开数据集设计器，然后双击要为其创建验证的列或表。 此操作将打开代码文件，你可在该文件中创建 <xref:System.Data.DataTable.ColumnChanging> 或 <xref:System.Data.DataTable.RowChanging> 事件处理程序。

```csharp
private static void OnColumnChanging(object sender, DataColumnChangeEventArgs e)
{

}
```

```vb
Private Shared Sub OnColumnChanging(sender As Object, e As DataColumnChangeEventArgs)
 
End Sub
```

## <a name="validate-data"></a>验证数据
数据集内的验证通过以下方式完成：

- 创建可以在更改过程中检查单个数据列中值的特定于应用程序的验证。 有关详细信息，请参阅[如何：在列更改过程中验证数据](validate-data-in-datasets.md)。

- 创建可以在整个数据行发生更改时将数据检查到值的特定于应用程序的验证。 有关详细信息，请参阅[如何：在行更改过程中验证数据](validate-data-in-datasets.md)。

- 创建键、唯一约束等，作为数据集实际架构定义的一部分。

- 设置 <xref:System.Data.DataColumn> 对象的属性，例如 <xref:System.Data.DataColumn.MaxLength%2A>、<xref:System.Data.DataColumn.AllowDBNull%2A> 和 <xref:System.Data.DataColumn.Unique%2A>。

当记录中发生更改时，<xref:System.Data.DataTable> 对象会引发多个事件：

- 每次更改单个列时和更改之后都会引发 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.ColumnChanged> 事件。 要验证特定列中的更改时，<xref:System.Data.DataTable.ColumnChanging> 事件很有用。 有关建议的更改的信息将作为参数传递到事件。
- 行中发生任何更改时和更改后，将引发 <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowChanged> 事件。 <xref:System.Data.DataTable.RowChanging> 事件更常见。 它表示行中某个位置正在发生更改，但不知道哪个列发生了更改。

默认情况下，对列的每个更改都将引发四个事件。 首先是更改的特定列的 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.ColumnChanged> 事件。 接下来是 <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowChanged> 事件。 如果对行进行了多项更改，则每次发生更改时都会引发事这些件。

> [!NOTE]
> 每个列发生更改后，数据行的 <xref:System.Data.DataRow.BeginEdit%2A> 方法会关闭 <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowChanged> 事件。 在这种情况下，在调用 <xref:System.Data.DataRow.EndEdit%2A> 方法之前，如果仅引发一次 <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowChanged> 事件，则不会引发事件。 有关详细信息，请参阅[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

你选择的事件取决于你希望的验证粒度。 如果在列发生更改时立即捕获错误很重要，请使用 <xref:System.Data.DataTable.ColumnChanging> 事件生成验证。 否则，请使用 <xref:System.Data.DataTable.RowChanging> 事件，这可能会导致同时捕获几个错误。 此外，如果你的数据是结构化的，以便根据另一列的内容来验证一列的值，请在 <xref:System.Data.DataTable.RowChanging> 事件期间执行验证。

更新记录后，<xref:System.Data.DataTable> 对象会引发事件，你可以在发生更改时和进行更改后响应这些事件。

如果你的应用程序使用类型化数据集，则可以创建强类型化事件处理程序。 这将添加你可为其创建处理程序的四个其他类型化事件：`dataTableNameRowChanging`、`dataTableNameRowChanged`、`dataTableNameRowDeleting` 和 `dataTableNameRowDeleted`。 这些类型化事件处理程序会传递一个参数，该参数包含表的列名，使代码更易于编写和读取。

## <a name="data-update-events"></a>数据更新事件

|事件|说明|
|-----------|-----------------|
|<xref:System.Data.DataTable.ColumnChanging>|列中的值正在更改。 事件向你传递行和列以及建议的新值。|
|<xref:System.Data.DataTable.ColumnChanged>|列中的值已更改。 事件向你传递行和列以及建议的值。|
|<xref:System.Data.DataTable.RowChanging>|对 <xref:System.Data.DataRow> 对象的更改将提交回数据集。 如果未调用 <xref:System.Data.DataRow.BeginEdit%2A> 方法，则在引发 <xref:System.Data.DataTable.ColumnChanging> 事件后，对列的每次更改后立即引发 <xref:System.Data.DataTable.RowChanging> 事件。 如果在进行更改之前调用 <xref:System.Data.DataRow.BeginEdit%2A>，则仅在调用 <xref:System.Data.DataRow.EndEdit%2A> 方法时引发 <xref:System.Data.DataTable.RowChanging> 事件。<br /><br /> 事件将行传递给你，并提供一个值，该值指示正在执行的操作类型（更改、插入等）。|
|<xref:System.Data.DataTable.RowChanged>|已更改行。 事件将行传递给你，并提供一个值，该值指示正在执行的操作类型（更改、插入等）。|
|<xref:System.Data.DataTable.RowDeleting>|正在删除行。 事件将行传递给你，并提供一个值，该值指示正在执行的操作类型（删除）。|
|<xref:System.Data.DataTable.RowDeleted>|已删除行。 事件将行传递给你，并提供一个值，该值指示正在执行的操作类型（删除）。|

在更新过程中会引发 <xref:System.Data.DataTable.ColumnChanging>、<xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowDeleting> 事件。 可以使用这些事件来验证数据或执行其他类型的处理。 由于在这些事件期间正在进行更新，因此你可以通过引发异常来取消更新，这会阻止更新完成。

<xref:System.Data.DataTable.ColumnChanged>、<xref:System.Data.DataTable.RowChanged> 和 <xref:System.Data.DataTable.RowDeleted> 事件是更新成功完成后引发的通知事件。 如果希望根据成功的更新执行进一步的操作，这些事件很有用。

## <a name="validate-data-during-column-changes"></a>在列更改过程中验证数据

> [!NOTE]
> 数据集设计器会创建分部类，可在其中将验证逻辑添加到数据集。 设计器生成的数据集不会删除或更改分部类中的任何代码。

数据列中的值更改时，可以通过响应 <xref:System.Data.DataTable.ColumnChanging> 事件来验证数据。 引发此事件时，它会传递事件参数 (<xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A>)，其中包含为当前列建议的值。 根据 `e.ProposedValue` 的内容，可以执行以下操作：

- 不执行任何操作，接受建议的值。

- 从更改列的事件处理程序中设置列错误 (<xref:System.Data.DataRow.SetColumnError%2A>)以拒绝建议的值。

- 可以使用 <xref:System.Windows.Forms.ErrorProvider> 控件向用户显示错误消息。 有关详细信息，请参阅 [ErrorProvider 组件](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms)。

在 <xref:System.Data.DataTable.RowChanging> 事件期间也可以执行验证。

## <a name="validate-data-during-row-changes"></a>在行更改过程中验证数据
可以编写代码以验证你要验证的每个列是否包含满足应用程序要求的数据。 设置列，使其在建议的值不可接受时包含错误，以完成此操作。 下面的示例在 `Quantity` 列等于或小于 0 时设置列错误。 更改行的事件处理程序应类似于以下示例。

### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>在行更改时验证数据 (Visual Basic)

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[演练：在数据集设计器中创建数据集](walkthrough-creating-a-dataset-with-the-dataset-designer.md)。

2. 双击要验证的表的标题栏。 此操作会在数据集的分部类文件中自动创建 <xref:System.Data.DataTable> 的 <xref:System.Data.DataTable.RowChanging> 事件处理程序。

    > [!TIP]
    > 双击表名称的左侧，以创建更改行的事件处理程序。 如果双击表名，你可以对其进行编辑。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataValidating/VB/NorthwindDataSet.vb" id="Snippet3":::

### <a name="to-validate-data-when-a-row-changes-c"></a>在行更改时验证数据 (C#)

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[演练：在数据集设计器中创建数据集](walkthrough-creating-a-dataset-with-the-dataset-designer.md)。

2. 双击要验证的表的标题栏。 此操作会为 <xref:System.Data.DataTable> 创建分部类文件。

    > [!NOTE]
    > 数据集设计器不会自动为 <xref:System.Data.DataTable.RowChanging> 事件创建事件处理程序。 必须创建处理 <xref:System.Data.DataTable.RowChanging> 事件的方法并运行代码，以在表的初始化方法中连接该事件。

3. 将以下代码复制到分部类：

    ```csharp
    public override void EndInit()
    {
        base.EndInit();
        Order_DetailsRowChanging += TestRowChangeEvent;
    }

    public void TestRowChangeEvent(object sender, Order_DetailsRowChangeEvent e)
    {
        if ((short)e.Row.Quantity <= 0)
        {
            e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");
        }
        else
        {
            e.Row.SetColumnError("Quantity", "");
        }
    }
    ```

## <a name="to-retrieve-changed-rows"></a>检索已更改的行
数据表中的每一行都有 <xref:System.Data.DataRow.RowState%2A> 属性，该属性使用 <xref:System.Data.DataRowState> 枚举中的值跟踪该行的当前状态。 可以通过调用 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 的 `GetChanges` 方法，从数据集或数据表返回已更改的行。 可以通过调用数据集的 <xref:System.Data.DataSet.HasChanges%2A> 方法来验证在调用 `GetChanges` 之前是否存在更改。

> [!NOTE]
> （通过调用 <xref:System.Data.DataSet.AcceptChanges%2A> 方法）提交对数据集或数据表的更改后，`GetChanges` 方法不会返回任何数据。 如果应用程序需要处理已更改的行，则必须在调用 `AcceptChanges` 方法之前处理这些更改。

调用数据集或数据表的 <xref:System.Data.DataSet.GetChanges%2A> 方法将返回仅包含已更改记录的新数据集或数据表。 如果要获取特定记录（例如仅新记录或仅经修改的记录），可以将来自 <xref:System.Data.DataRowState> 枚举的值作为参数传递给 `GetChanges` 方法。

使用 <xref:System.Data.DataRowVersion> 枚举访问行的其他版本（例如，处理行之前存在于行中的原始值）。

### <a name="to-get-all-changed-records-from-a-dataset"></a>从数据集获取所有已更改的记录

- 调用数据集的 <xref:System.Data.DataSet.GetChanges%2A> 方法。

     下面的示例会创建名为 `changedRecords` 的新数据集，并用另一个名为 `dataSet1` 的数据集中的所有已更改记录填充它。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet14":::

### <a name="to-get-all-changed-records-from-a-data-table"></a>从数据表获取所有已更改的记录

- 调用 DataTable 的 <xref:System.Data.DataTable.GetChanges%2A> 方法。

     下面的示例将创建名为 `changedRecordsTable` 的新数据表，并使用另一个名为 `dataTable1` 的数据表中已更改的所有记录填充它。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet15":::

### <a name="to-get-all-records-that-have-a-specific-row-state"></a>获取具有特定行状态的所有记录

- 调用数据集或数据表的 `GetChanges` 方法，并以参数的形式传递 <xref:System.Data.DataRowState> 枚举值。

     下面的示例演示如何创建名为 `addedRecords` 的新数据集，并使用已添加到 `dataSet1` 数据集的记录来填充它。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet16":::

     下面的示例演示如何返回最近添加到 `Customers` 表中的所有记录：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet17":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet17":::

## <a name="access-the-original-version-of-a-datarow"></a>访问 DataRow 的原始版本
对数据行进行更改时，数据集将保留该行的原始版本 (<xref:System.Data.DataRowVersion.Original>) 和新版本 (<xref:System.Data.DataRowVersion.Current>)。 例如，在调用 `AcceptChanges` 方法之前，应用程序可以访问记录的不同版本（如 <xref:System.Data.DataRowVersion> 枚举中所定义），并相应地处理更改。

> [!NOTE]
> 行的不同版本仅在编辑行后、调用 `AcceptChanges` 方法之前存在。 调用 `AcceptChanges` 方法后，当前版本和原始版本相同。

传递 <xref:System.Data.DataRowVersion> 值连同列索引（或列名称作为字符串）将从该列的特定行版本返回值。 在 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.ColumnChanged> 事件期间，会标识已更改的列。 这是检查行的不同版本以进行验证的好时机。 但是，如果你暂时挂起了约束，则不会引发这些事件，将需要以编程方式标识哪些列已更改。 为此，可以循环访问 <xref:System.Data.DataTable.Columns%2A> 集合并比较不同的 <xref:System.Data.DataRowVersion> 值。

### <a name="to-get-the-original-version-of-a-record"></a>获取记录的原始版本

- 通过传入要返回的行的 <xref:System.Data.DataRowVersion> 来访问列的值。

     下面的示例演示如何使用 <xref:System.Data.DataRowVersion> 值获取 <xref:System.Data.DataRow> 中 `CompanyName` 字段的原始值：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet21":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet21":::

## <a name="access-the-current-version-of-a-datarow"></a>访问 DataRow 的当前版本

### <a name="to-get-the-current-version-of-a-record"></a>获取记录的当前版本

- 访问列的值，然后向索引添加一个参数，用于指示要返回行的哪个版本。

     下面的示例演示如何使用 <xref:System.Data.DataRowVersion> 值获取 <xref:System.Data.DataRow> 中 `CompanyName` 字段的当前值：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet22":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet22":::

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [如何：在 Windows 窗体 DataGridView 控件中验证数据](/dotnet/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control)
- [如何：使用 Windows 窗体 ErrorProvider 组件为窗体验证显示错误图标](/dotnet/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider)
