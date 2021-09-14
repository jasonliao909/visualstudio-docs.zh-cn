---
title: 向 n 层数据集添加验证
description: 向 Visual Studio 中的 n 层数据集添加Visual Studio。 验证对单个列或整行的更改。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601235"
---
# <a name="add-validation-to-an-n-tier-dataset"></a>向 n 层数据集添加验证
将验证添加到隔离到 n 层解决方案的数据集基本上与将验证添加到单文件数据集 (单个项目中的数据集添加) 。 对数据执行验证的建议位置是在数据表的 <xref:System.Data.DataTable.ColumnChanging> 和/或 <xref:System.Data.DataTable.RowChanging> 事件期间。

数据集提供创建分部类的功能，可以将用户代码添加到数据集中数据表的列更改和行更改事件。 有关将代码添加到 n 层解决方案中的数据集的信息，请参阅将代码添加到[n](../data-tools/add-code-to-datasets-in-n-tier-applications.md)层应用程序中的数据集和将代码添加到 n 层应用程序中的[TableAdapters。](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md) 有关分部类详细信息，请参阅 [如何：将 ](../ide/class-designer/how-to-split-a-class-into-partial-classes.md) 类拆分为分部 (类设计器) [或分部类和方法](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)。

> [!NOTE]
> 通过设置 **DataSet** Project 属性 (TableAdapters) ，不会自动移动项目中的现有分部数据集类。 必须将现有分部数据集类手动移动到数据集项目。

> [!NOTE]
> 数据集设计器不会自动在 C# 中为 和 <xref:System.Data.DataTable.ColumnChanging> 事件创建 <xref:System.Data.DataTable.RowChanging> 事件处理程序。 必须手动创建事件处理程序，将事件处理程序挂钩到基础事件。 以下过程介绍如何在 Visual Basic 和 C# 中创建所需的事件处理程序。

## <a name="validate-changes-to-individual-columns"></a>验证对单个列的更改
通过处理 事件来验证各个列中 <xref:System.Data.DataTable.ColumnChanging> 的值。 <xref:System.Data.DataTable.ColumnChanging>修改列中的值时，将引发 事件。 通过双击事件上的所需列，为事件 <xref:System.Data.DataTable.ColumnChanging> 创建数据集设计器。 

首次双击列时，设计器会为事件生成事件 <xref:System.Data.DataTable.ColumnChanging> 处理程序。 还会 `If...Then` 创建一个语句，用于测试特定列。 例如，双击 Northwind Orders 表上的 **RequiredDate** 列时，将生成以下代码：

```vb
Private Sub OrdersDataTable_ColumnChanging(ByVal sender As System.Object, ByVal e As System.Data.DataColumnChangeEventArgs) Handles Me.ColumnChanging
    If (e.Column.ColumnName = Me.RequiredDateColumn.ColumnName) Then
        ' Add validation code here.
    End If
End Sub
```

> [!NOTE]
> 在 C# 项目中，数据集设计器为数据集和数据集中的单个表创建分部类。 该数据集设计器在 C# 中不会自动为 和 事件创建事件处理程序，就像在 Visual Basic <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 中一样。 在 C# 项目中，必须手动构造一个方法来处理事件，并且将方法挂接到基础事件。 以下过程提供了在 Visual Basic 和 C# 中创建所需事件处理程序的步骤。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-add-validation-during-changes-to-individual-column-values"></a>在更改单个列值期间添加验证

1. 在 中双击 *.xsd* 文件，打开 **解决方案资源管理器。** 有关详细信息，请参阅 [演练：在](walkthrough-creating-a-dataset-with-the-dataset-designer.md)数据集设计器。

2. 双击要验证的列。 此操作将创建 <xref:System.Data.DataTable.ColumnChanging> 事件处理程序。

    > [!NOTE]
    > 该数据集设计器不会自动为 C# 事件创建事件处理程序。 下一部分包含处理 C# 中的事件所需的代码。 `SampleColumnChangingEvent` 创建 ，然后挂接到 <xref:System.Data.DataTable.ColumnChanging> 方法中的 <xref:System.Data.DataTable.EndInit%2A> 事件。

3. 添加代码以验证 `e.ProposedValue` 是否包含满足应用程序要求的数据。 如果建议的值不可接受，请设置 列以指示它包含错误。

     下面的代码示例验证 **Quantity** 列是否包含大于 0 的值。 如果 **Quantity** 小于或等于 0，则列设置为错误。 如果 `Else` Quantity 大于 0，则 子句将清除错误。  列更改事件处理程序中的代码应如下所示：

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
通过处理 事件验证整行 <xref:System.Data.DataTable.RowChanging> 中的值。 提交 <xref:System.Data.DataTable.RowChanging> 所有列中的值时，将引发 事件。 当一列中的值依赖于另一列中的值时， <xref:System.Data.DataTable.RowChanging> 需要验证 事件。 例如，请考虑 Northwind 的 Orders 表中的 OrderDate 和 RequiredDate。

输入订单时，验证确保订单不是使用 OrderDate 上或之前为 RequiredDate 输入的。 本示例需要比较 RequiredDate 和 OrderDate 列的值，因此验证单个列更改没有意义。

通过双击事件上表的标题栏中的表名，为 <xref:System.Data.DataTable.RowChanging> 事件创建数据集设计器。 

#### <a name="to-add-validation-during-changes-to-whole-rows"></a>在更改整个行期间添加验证

1. 在 中双击 *.xsd* 文件，打开 **解决方案资源管理器。** 有关详细信息，请参阅 [演练：在](walkthrough-creating-a-dataset-with-the-dataset-designer.md)数据集设计器。

2. 双击设计器上数据表的标题栏。

     分部类使用事件处理程序 `RowChanging` 创建，在代码编辑器中打开。

    > [!NOTE]
    > 该数据集设计器不会自动为 <xref:System.Data.DataTable.RowChanging> C# 项目中的事件创建事件处理程序。 必须创建一个方法来处理事件并运行代码，然后在表的初始化方法中 <xref:System.Data.DataTable.RowChanging> 挂接该事件。

3. 在分部类声明中添加用户代码。

4. 以下代码显示了在事件期间添加要验证的用户代码 <xref:System.Data.DataTable.RowChanging> 位置。 C# 示例还包括用于将事件处理程序方法挂钩到事件 `OrdersRowChanging` 的代码。

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
