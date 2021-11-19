---
title: 向 n 层数据集添加验证
description: 向 Visual Studio 中的 n 层数据集添加验证。 验证对单个列或整行的更改。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, validating
- validation [Visual Basic], n-tier data applications
- validating n-tier data applications
ms.assetid: 34ce4db6-09bb-4b46-b435-b2514aac52d3
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 6d9774b45743b57941d08903375d29b663b64192
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601235"
---
# <a name="add-validation-to-an-n-tier-dataset"></a>向 n 层数据集添加验证
向分离为 n 层解决方案的数据集添加验证与向单文件数据集（单个项目中的数据集）添加验证基本相同。 建议在数据表的 <xref:System.Data.DataTable.ColumnChanging> 和/或 <xref:System.Data.DataTable.RowChanging> 事件期间执行数据验证。

数据集可以创建分部类，在其中你可以将用户代码添加到数据集中数据表的列更改和行更改事件。 有关向 n 层解决方案中的数据集添加代码的详细信息，请参阅[向 n 层应用程序中的数据集添加代码](../data-tools/add-code-to-datasets-in-n-tier-applications.md)和[ n 层应用程序中的 TableAdapters 添加代码](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)。 有关分部类的详细信息，请参阅[如何：将类拆分为分部类（类设计器）](../ide/class-designer/how-to-split-a-class-into-partial-classes.md)或[分部类和方法](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)。

> [!NOTE]
> 分离数据集与 TableAdapter（通过设置“数据集项目”属性）时，不会自动移动项目中现有的数据集分部类。 必须手动将现有的分部数据集类移动到数据集项目。

> [!NOTE]
> 数据集设计器不会在 C# 中为 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.RowChanging> 事件自动创建事件处理程序。 必须手动创建事件处理程序并将其与底层事件连接起来。 以下过程说明如何在 Visual Basic 和 C# 中创建所需的事件处理程序。

## <a name="validate-changes-to-individual-columns"></a>验证对单个列的更改
通过处理 <xref:System.Data.DataTable.ColumnChanging> 事件验证单个列中的值。 修改列中的值时会引发 <xref:System.Data.DataTable.ColumnChanging> 事件。 双击数据集设计器上的所需列，为 <xref:System.Data.DataTable.ColumnChanging> 事件创建事件处理程序。

第一次双击列时，设计器会为 <xref:System.Data.DataTable.ColumnChanging> 事件生成事件处理程序。 还会创建 `If...Then` 语句来测试特定列。 例如，双击 Northwind Orders 表上的 RequiredDate 列时，会生成以下代码：

```vb
Private Sub OrdersDataTable_ColumnChanging(ByVal sender As System.Object, ByVal e As System.Data.DataColumnChangeEventArgs) Handles Me.ColumnChanging
    If (e.Column.ColumnName = Me.RequiredDateColumn.ColumnName) Then
        ' Add validation code here.
    End If
End Sub
```

> [!NOTE]
> 在 C# 项目中，数据集设计器仅为数据集和数据集中的单个表创建分部类。 数据集设计器不会像在 Visual Basic 中那样自动为 C# 中的 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.RowChanging> 事件创建事件处理程序。 在 C# 项目中，必须手动构造处理事件的方法并将其与底层事件连接起来。 以下过程分步说明如何在 Visual Basic 和 C# 中创建所需的事件处理程序。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-add-validation-during-changes-to-individual-column-values"></a>在更改单个列值时添加验证

1. 在解决方案资源管理器中双击 .xsd 文件，打开数据集。 有关详细信息，请参阅[演练：在数据集设计器中创建数据集](walkthrough-creating-a-dataset-with-the-dataset-designer.md)。

2. 双击要验证的列。 该操作会创建 <xref:System.Data.DataTable.ColumnChanging> 事件处理程序。

    > [!NOTE]
    > 数据集设计器不会自动为 C# 事件创建事件处理程序。 处理 C# 事件所需的代码在下一部分中说明。 `SampleColumnChangingEvent` 在创建后会与 <xref:System.Data.DataTable.EndInit%2A> 方法中的 <xref:System.Data.DataTable.ColumnChanging> 事件连接起来。

3. 添加代码，验证 `e.ProposedValue` 是否包含符合应用程序需求的数据。 如果建议的值不可接受，请设置该列以指示其包含一个错误。

     以下代码示例验证 Quantity 列是否包含大于 0 的值。 如果 Quantity 小于或等于 0，则将列设置为包含错误。 如果 Quantity 大于 0，则 `Else` 子句会清除错误。 列更改事件处理程序中的代码应如下所示：

    ```vb
    If (e.Column.ColumnName = Me.QuantityColumn.ColumnName) Then
        If CType(e.ProposedValue, Short) <= 0 Then
            e.Row.SetColumnError(e.Column, "Quantity must be greater than 0")
        Else
            e.Row.SetColumnError(e.Column, "")
        End If
    End If
    ```

    ```csharp
    // Add this code to the DataTable partial class.

    public override void EndInit()
    {
        base.EndInit();
        // Hook up the ColumnChanging event
        // to call the SampleColumnChangingEvent method.
        ColumnChanging += SampleColumnChangingEvent;
    }

    public void SampleColumnChangingEvent(object sender, System.Data.DataColumnChangeEventArgs e)
    {
        if (e.Column.ColumnName == QuantityColumn.ColumnName)
        {
            if ((short)e.ProposedValue <= 0)
            {
                e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");
            }
            else
            {
                e.Row.SetColumnError("Quantity", "");
            }
        }
    }
    ```

## <a name="validate-changes-to-whole-rows"></a>验证对整行的更改
通过处理 <xref:System.Data.DataTable.RowChanging> 事件验证整行中的值。 提交所有列中的值时，会引发 <xref:System.Data.DataTable.RowChanging> 事件。 某一列中的值依赖另一列中的值时，需在 <xref:System.Data.DataTable.RowChanging> 事件中进行验证。 例如，以 Northwind 的 Orders 表中的 OrderDate 和 RequiredDate 为例。

输入订单时，验证可确保输入的订单的 RequiredDate 晚于 OrderDate。 在此示例中，需比较 RequiredDate 和 OrderDate 列的值，因此对单个列更改进行验证没有意义。

双击数据集设计器上表格标题栏中的表格名称，为 <xref:System.Data.DataTable.RowChanging> 事件创建事件处理程序。

#### <a name="to-add-validation-during-changes-to-whole-rows"></a>在更改整个行时添加验证

1. 在解决方案资源管理器中双击 .xsd 文件，打开数据集。 有关详细信息，请参阅[演练：在数据集设计器中创建数据集](walkthrough-creating-a-dataset-with-the-dataset-designer.md)。

2. 双击设计器上数据表的标题栏。

     分部类是随 `RowChanging` 事件处理程序创建的，并且在代码编辑器中打开。

    > [!NOTE]
    > 数据集设计器不会自动为 C# 项目中的 <xref:System.Data.DataTable.RowChanging> 事件创建事件处理程序。 必须创建处理 <xref:System.Data.DataTable.RowChanging> 事件的方法并运行代码，然后在表的初始化方法中连接该事件。

3. 将用户代码添加到分部类声明中。

4. 以下代码显示什么情况下在 <xref:System.Data.DataTable.RowChanging> 事件期间添加要验证的用户代码。 C# 示例还包括将事件处理程序方法连接到 `OrdersRowChanging` 事件的代码。

    ```vb
    Partial Class OrdersDataTable
        Private Sub OrdersDataTable_OrdersRowChanging(ByVal sender As System.Object, ByVal e As OrdersRowChangeEvent) Handles Me.OrdersRowChanging
            ' Add logic to validate columns here.
            If e.Row.RequiredDate <= e.Row.OrderDate Then
                ' Set the RowError if validation fails.
                e.Row.RowError = "Required Date cannot be on or before the OrderDate"
            Else
                ' Clear the RowError when validation passes.
                e.Row.RowError = ""
            End If
        End Sub
    End Class
    ```

    ```csharp
    partial class OrdersDataTable
    {
        public override void EndInit()
        {
            base.EndInit();
            // Hook up the event to the
            // RowChangingEvent method.
            OrdersRowChanging += RowChangingEvent;
        }

        public void RowChangingEvent(object sender, OrdersRowChangeEvent e)
        {
            // Perform the validation logic.
            if (e.Row.RequiredDate <= e.Row.OrderDate)
            {
                // Set the row to an error when validation fails.
                e.Row.RowError = "Required Date cannot be on or before the OrderDate";
            }
            else
            {
                // Clear the RowError if validation passes.
                e.Row.RowError = "";
            }
        }
    }
    ```

## <a name="see-also"></a>另请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [演练：创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [验证数据集中的数据](../data-tools/validate-data-in-datasets.md)
