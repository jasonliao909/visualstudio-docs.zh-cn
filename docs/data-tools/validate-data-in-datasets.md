---
title: 验证数据集中的数据
description: 了解如何验证数据集中的数据。 验证数据涉及确认输入到数据对象中的值是否符合数据集架构中的约束。
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
ms.openlocfilehash: a9f714b4e66f14e313fa53466db80c99dfbef50f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601065"
---
# <a name="validate-data-in-datasets"></a>验证数据集中的数据
验证数据是确认输入到数据对象中的值是否符合数据集架构中的约束的过程。 验证过程还确认这些值是否遵循为应用程序建立的规则。 在将更新发送到基础数据库之前验证数据是一种很好的做法。 这可以减少错误以及应用程序和数据库之间的潜在往返次数。

可以通过在数据集本身中生成验证检查来确认写入数据集的数据是否有效。 无论更新执行方式如何，数据集都可以检查数据 - 无论是直接由窗体中的控件、组件内控件还是以其他方式执行。 由于数据集是应用程序库的一 (数据库后端) ，因此它是生成特定于应用程序的验证的逻辑位置。

向应用程序添加验证的最佳位置是数据集的分部类文件。 在 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 或 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 中 **，数据集设计器** 并双击要创建验证的列或表。 此操作会自动创建 或 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 事件处理程序。

## <a name="validate-data"></a>验证数据
数据集中的验证通过以下方式完成：

- 通过创建自己的特定于应用程序的验证，可以在更改期间检查单个数据列中的值。 有关详细信息，请参阅 [如何：在列更改期间验证数据](validate-data-in-datasets.md)。

- 通过创建自己的特定于应用程序的验证，可以在更改整个数据行时将数据检查为值。 有关详细信息，请参阅 [如何：在行更改期间验证数据](validate-data-in-datasets.md)。

- 通过创建键、唯一约束等作为数据集的实际架构定义的一部分。

- 通过设置 对象 <xref:System.Data.DataColumn> 的属性，例如 、 和 <xref:System.Data.DataColumn.MaxLength%2A> <xref:System.Data.DataColumn.AllowDBNull%2A> <xref:System.Data.DataColumn.Unique%2A> 。

当记录中发生 <xref:System.Data.DataTable> 更改时，对象将引发多个事件：

- 每次 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.ColumnChanged> 更改单个列期间和之后，将引发 和 事件。 想要 <xref:System.Data.DataTable.ColumnChanging> 验证特定列中的更改时，事件非常有用。 有关建议更改的信息作为参数与 事件一起传递。
- 和 <xref:System.Data.DataTable.RowChanging> <xref:System.Data.DataTable.RowChanged> 事件在行的任何更改期间和之后引发。 事件 <xref:System.Data.DataTable.RowChanging> 更通用。 它指示行中的某一位置发生了更改，但不知道更改了哪个列。

默认情况下，对列的每个更改都引发四个事件。 第一 <xref:System.Data.DataTable.ColumnChanging> 种是要 <xref:System.Data.DataTable.ColumnChanged> 更改的特定列的 和 事件。 接下来是 <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowChanged> 事件。 如果对行进行多次更改，将针对每次更改引发事件。

> [!NOTE]
> 数据行的 <xref:System.Data.DataRow.BeginEdit%2A> 方法在每个单独的列更改 <xref:System.Data.DataTable.RowChanging> 后关闭 和 <xref:System.Data.DataTable.RowChanged> 事件。 在这种情况下，当 和 事件只引发一次时，在调用 方法之前 <xref:System.Data.DataRow.EndEdit%2A> <xref:System.Data.DataTable.RowChanging> <xref:System.Data.DataTable.RowChanged> 不会引发 事件。 有关详细信息，请参阅 [在填充数据集 时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

选择的事件取决于验证的粒度。 如果列发生更改时立即捕获错误很重要，则使用 事件生成 <xref:System.Data.DataTable.ColumnChanging> 验证。 否则，请使用 <xref:System.Data.DataTable.RowChanging> 事件，这可能会导致一次捕获多个错误。 此外，如果数据是结构化的，以便基于另一列的内容验证一列的值，请执行事件期间 <xref:System.Data.DataTable.RowChanging> 验证。

更新记录时，对象将引发事件，可以在发生更改时和进行更改 <xref:System.Data.DataTable> 后响应这些事件。

如果应用程序使用类型数据集，可以创建强类型事件处理程序。 这会添加四个可创建处理程序的其他类型事件 `dataTableNameRowChanging` `dataTableNameRowChanged` `dataTableNameRowDeleting` ：、、 和 `dataTableNameRowDeleted` 。 这些类型事件处理程序传递一个参数，该参数包含表的列名，使代码更易于编写和读取。

## <a name="data-update-events"></a>数据更新事件

|事件|说明|
|-----------|-----------------|
|<xref:System.Data.DataTable.ColumnChanging>|列中的值正在更改。 事件将行和列以及建议的新值传递给你。|
|<xref:System.Data.DataTable.ColumnChanged>|列中的值已更改。 事件将行和列以及建议的值传递给你。|
|<xref:System.Data.DataTable.RowChanging>|对 对象所做的更改 <xref:System.Data.DataRow> 即将提交回数据集。 如果尚未调用 方法，则引发事件后立即针对列的每个更改 <xref:System.Data.DataRow.BeginEdit%2A> <xref:System.Data.DataTable.RowChanging> 引发 <xref:System.Data.DataTable.ColumnChanging> 事件。 如果在进行更改 <xref:System.Data.DataRow.BeginEdit%2A> 之前调用 ，则仅在调用 方法 <xref:System.Data.DataTable.RowChanging> 时引发 <xref:System.Data.DataRow.EndEdit%2A> 事件。<br /><br /> 事件将行以及一个值传递给你，该值指示要执行 (插入等操作) 类型。|
|<xref:System.Data.DataTable.RowChanged>|行已更改。 事件将行以及一个值传递给你，该值指示要执行 (插入等操作) 类型。|
|<xref:System.Data.DataTable.RowDeleting>|正在删除行。 事件将行以及一个值传递给你，该值指示要执行 (删除) 类型。|
|<xref:System.Data.DataTable.RowDeleted>|已删除行。 事件将行以及一个值传递给你，该值指示要执行 (删除) 类型。|

、 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 和 <xref:System.Data.DataTable.RowDeleting> 事件在更新过程中引发。 可以使用这些事件来验证数据或执行其他类型的处理。 由于更新在这些事件期间进行中，因此可以通过引发异常来取消更新，从而阻止更新完成。

、 <xref:System.Data.DataTable.ColumnChanged> <xref:System.Data.DataTable.RowChanged> <xref:System.Data.DataTable.RowDeleted> 和 事件是更新成功完成后引发的通知事件。 当你想要根据成功的更新采取进一步操作时，这些事件非常有用。

## <a name="validate-data-during-column-changes"></a>在列更改期间验证数据

> [!NOTE]
> 该 **数据集设计器** 创建一个分部类，可在其中将验证逻辑添加到数据集。 设计器生成的数据集不会删除或更改分部类中的任何代码。

当数据列中的值更改时，可以通过响应 事件来验证 <xref:System.Data.DataTable.ColumnChanging> 数据。 引发此事件时，会将事件参数 () 包含为当前列建议 <xref:System.Data.DataColumnChangeEventArgs.ProposedValue%2A> 的值的值。 根据 的内容 `e.ProposedValue` ，你可以：

- 不执行任何操作来接受建议的值。

- 通过从列更改事件处理程序 () 列错误值来拒绝 <xref:System.Data.DataRow.SetColumnError%2A> 建议的值。

- （可选） <xref:System.Windows.Forms.ErrorProvider> 使用 控件向用户显示错误消息。 有关详细信息，请参阅 [ErrorProvider 组件](/dotnet/framework/winforms/controls/errorprovider-component-windows-forms)。

还可以在事件期间执行 <xref:System.Data.DataTable.RowChanging> 验证。

## <a name="validate-data-during-row-changes"></a>在行更改期间验证数据
可以编写代码来验证要验证的每个列是否包含满足应用程序要求的数据。 为此，请设置 列，以指示如果建议的值不可接受，则包含错误。 以下示例在列为 0 或更低时 `Quantity` 设置列错误。 行更改事件处理程序应类似于以下示例。

### <a name="to-validate-data-when-a-row-changes-visual-basic"></a>在行更改时验证 (Visual Basic) 

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅演练： [在](walkthrough-creating-a-dataset-with-the-dataset-designer.md)数据集设计器。

2. 双击要验证的表的标题栏。 此操作会自动在 <xref:System.Data.DataTable.RowChanging> 数据集的分部类文件中创建 <xref:System.Data.DataTable> 的事件处理程序。

    > [!TIP]
    > 双击表名称左侧以创建行更改事件处理程序。 如果双击表名称，可以对其进行编辑。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataValidating/VB/NorthwindDataSet.vb" id="Snippet3":::

### <a name="to-validate-data-when-a-row-changes-c"></a>在行更改时验证 C# () 

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅 [演练：在](walkthrough-creating-a-dataset-with-the-dataset-designer.md)数据集设计器。

2. 双击要验证的表的标题栏。 此操作为 创建分部类文件 <xref:System.Data.DataTable> 。

    > [!NOTE]
    > 该 **数据集设计器** 不会自动为事件创建事件 <xref:System.Data.DataTable.RowChanging> 处理程序。 必须创建一个方法来处理事件，并运行代码以挂接表的初始化方法 <xref:System.Data.DataTable.RowChanging> 中的事件。

3. 将以下代码复制到分部类中：

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

## <a name="to-retrieve-changed-rows"></a>检索更改的行
数据表中的每一行都有一个 属性，该属性使用 枚举中的值跟踪该行 <xref:System.Data.DataRow.RowState%2A> 的当前 <xref:System.Data.DataRowState> 状态。 可以通过调用 或 的 方法，从数据集或数据表中 `GetChanges` 返回更改 <xref:System.Data.DataSet> 的行 <xref:System.Data.DataTable> 。 在调用数据集的 方法之前，可以验证 `GetChanges` <xref:System.Data.DataSet.HasChanges%2A> 更改是否存在。

> [!NOTE]
> 通过调用 (方法将更改提交到数据集或数据表 <xref:System.Data.DataSet.AcceptChanges%2A> `GetChanges`) ，该方法不会返回任何数据。 如果应用程序需要处理更改的行，则必须在调用 方法之前处理 `AcceptChanges` 更改。

调用数据集或数据表的 方法将返回仅包含已更改记录的新数据集 <xref:System.Data.DataSet.GetChanges%2A> 或数据表。 如果要获取特定记录（例如，仅获取新记录或仅修改的记录），可以将枚举中的值作为参数传递给 <xref:System.Data.DataRowState> `GetChanges` 方法。

使用 枚举访问行的不同版本 (例如，在处理行之前，行中的原始值 <xref:System.Data.DataRowVersion>) 。

### <a name="to-get-all-changed-records-from-a-dataset"></a>从数据集获取所有更改的记录

- 调用 <xref:System.Data.DataSet.GetChanges%2A> 数据集的 方法。

     以下示例创建名为 的新数据集，并使用另一个数据集中所有已更改 `changedRecords` 的记录填充该数据集 `dataSet1` 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet14":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet14":::

### <a name="to-get-all-changed-records-from-a-data-table"></a>从数据表中获取所有更改的记录

- 调用 <xref:System.Data.DataTable.GetChanges%2A> DataTable 的 方法。

     以下示例创建名为 的新数据表，并使用另一个数据表中的所有更改 `changedRecordsTable` 记录填充该表 `dataTable1` 。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet15":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet15":::

### <a name="to-get-all-records-that-have-a-specific-row-state"></a>获取具有特定行状态的所有记录

- 调用 `GetChanges` 数据集或数据表的 方法，并传递 <xref:System.Data.DataRowState> 枚举值作为参数。

     以下示例演示如何创建名为 的新数据集，并仅用已添加到数据集的记录 `addedRecords` 填充 `dataSet1` 该数据集。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet16":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet16":::

     以下示例演示如何返回最近添加到表中的所有 `Customers` 记录：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet17":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet17":::

## <a name="access-the-original-version-of-a-datarow"></a>访问 DataRow 的原始版本
对数据行进行更改时，数据集将保留原始 () 行 () <xref:System.Data.DataRowVersion.Original> <xref:System.Data.DataRowVersion.Current> 行的新版本。 例如，在调用 方法之前，应用程序可以访问枚举 (中定义的不同版本的) 并相应地处理 `AcceptChanges` <xref:System.Data.DataRowVersion> 更改。

> [!NOTE]
> 行的不同版本仅在编辑后以及调用 方法之前 `AcceptChanges` 存在。 调用 `AcceptChanges` 方法后，当前版本和原始版本相同。

将值与列索引一起 (或列名称作为字符串) 返回该列的特定 <xref:System.Data.DataRowVersion> 行版本中的值。 更改的列在 和 <xref:System.Data.DataTable.ColumnChanging> 事件期间 <xref:System.Data.DataTable.ColumnChanged> 标识。 这是检查不同行版本以进行验证的不错时间。 但是，如果暂时挂起了约束，则这些事件不会引发，并且你需要以编程方式标识已更改的列。 为此，可以浏览集合 <xref:System.Data.DataTable.Columns%2A> 并比较不同的 <xref:System.Data.DataRowVersion> 值。

### <a name="to-get-the-original-version-of-a-record"></a>获取记录的原始版本

- 通过传递要返回的行的 来 <xref:System.Data.DataRowVersion> 访问列的值。

     下面的示例演示如何使用 值获取 <xref:System.Data.DataRowVersion> 中的 `CompanyName` 字段的原始值 <xref:System.Data.DataRow> ：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet21":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet21":::

## <a name="access-the-current-version-of-a-datarow"></a>访问 DataRow 的当前版本

### <a name="to-get-the-current-version-of-a-record"></a>获取记录的当前版本

- 访问列的值，然后将参数添加到索引中，该索引指示要返回的行版本。

     下面的示例演示如何使用 值 <xref:System.Data.DataRowVersion> 获取 中的字段 `CompanyName` 的当前值 <xref:System.Data.DataRow> ：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet22":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet22":::

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [如何：验证 Windows 窗体 DataGridView 控件中的数据](/dotnet/framework/winforms/controls/how-to-validate-data-in-the-windows-forms-datagridview-control)
- [如何：使用 Windows Forms ErrorProvider 组件显示表单验证的错误图标](/dotnet/framework/winforms/controls/display-error-icons-for-form-validation-with-wf-errorprovider)
