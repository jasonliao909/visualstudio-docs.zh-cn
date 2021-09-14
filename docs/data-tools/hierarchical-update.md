---
title: 分层更新
description: 查看分层更新，其中涉及将更新 (数据从包含 2 多个相关表的数据集保存) 返回到数据库，同时保留引用完整性规则。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- saving data, changed data
- data [Visual Basic], hierarchical update
- saving updated data
- datasets [Visual Basic], hierarchical update
- hierarchical update
- saving data, hierarchical update
- modified data saving
- updated data saving
- related tables, saving
ms.assetid: 68bae3f6-ec9b-45ee-a33a-69395029f54c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 74e96bf3644d57235aff82fb2b0393c1506dd653
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601154"
---
# <a name="hierarchical-update"></a>分层更新

*分层更新* 是指从包含两 (相关表的数据集中保存更新的数据的过程，) 返回到数据库，同时维护引用完整性规则。 *引用完整性* 是指数据库中约束提供的一致性规则，这些约束控制插入、更新和删除相关记录的行为。 例如，引用完整性强制在允许为客户创建订单之前创建客户记录。  有关数据集中的关系详细信息，请参阅 [数据集中的关系](../data-tools/relationships-in-datasets.md)。

分层更新功能使用 `TableAdapterManager` 管理 `TableAdapter` 类型化数据集中的 。 组件 `TableAdapterManager` 是一Visual Studio生成的类，而不是 .NET 类型。 将表从"数据源"窗口拖动到"Windows 窗体"或"WPF"页时，Visual Studio 会将 TableAdapterManager 类型的变量添加到窗体或页面，在组件栏中的设计器中可以看到它。 有关 类的详细信息 `TableAdapterManager` ，请参阅 TableAdapters 的 TableAdapterManager [Reference 部分](../data-tools/create-and-configure-tableadapters.md)。

默认情况下，数据集将相关表视为"仅关系"，这意味着它不会强制实施外键约束。 可以在设计时通过使用 属性来修改 **数据集设计器。** 选择两个表之间的关系线，打开" **关系"** 对话框。 在此处所做的更改将确定 在将相关表中的更改发送回数据库时 `TableAdapterManager` 的行为方式。

## <a name="enable-hierarchical-update-in-a-dataset"></a>在数据集中启用分层更新

默认情况下，为项目中添加或创建的所有新数据集启用分层更新。 将数据集中类型化数据集的 **"** 分层更新"属性设置为 **"True"** 或 **"False"，** 打开或关闭分层更新：

![分层更新设置](../data-tools/media/hierarchical-update-setting.png)

## <a name="create-a-new-relation-between-tables"></a>在表之间创建新关系

若要在两个表之间创建新关系，请在数据集设计器选择每个表的标题栏，然后右键单击并选择"添加 **关系"。**

![分层更新"添加关系"菜单](../data-tools/media/hierarchical-update-add-relation-menu.png)

## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>了解外键约束、级联更新和删除

必须了解如何在生成的数据集代码中创建数据库中的外键约束和级联行为。

默认情况下，数据集中的数据表是使用与数据库中 () <xref:System.Data.DataRelation> 关系关系一起生成的。 但是，数据集中的关系不会作为外键约束生成。 配置为 <xref:System.Data.DataRelation> "仅关系 **"，** 且 <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> 没有或 <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> 有效。

默认情况下，即使数据库关系设置为启用级联更新和/或级联删除，级联更新和级联删除也已关闭。 例如，创建新客户和新订单，然后尝试保存数据可能会导致与数据库中定义的外键约束冲突。 有关详细信息，请参阅 [在填充数据集 时关闭约束](turn-off-constraints-while-filling-a-dataset.md)。

## <a name="set-the-order-to-perform-updates"></a>设置执行更新的顺序

设置执行更新的顺序会设置将所有已修改数据保存在数据集的所有表中所需的单个插入、更新和删除的顺序。 启用分层更新后，首先执行插入，然后更新，然后删除。 `TableAdapterManager`提供一 `UpdateOrder` 个 属性，该属性可设置为先执行更新，然后插入，然后删除。

> [!NOTE]
> 必须了解，更新顺序包含所有内容。 也就是说，执行更新时，对数据集中所有表执行插入和删除操作。

若要设置 属性，请在将项从"数据源窗口"拖动到窗体后，选择组件栏中的 ，然后在"属性" `UpdateOrder` [](add-new-data-sources.md#data-sources-window) `TableAdapterManager` `UpdateOrder` 窗口中 **设置** 属性。

## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>在执行分层更新之前创建数据集的备份副本

通过调用 (方法) ，尝试在单个事务中更新每个表 `TableAdapterManager.UpdateAll()` `TableAdapterManager` 的数据。 如果任何表的更新的任何部分失败，则回滚整个事务。 在大多数情况下，回滚将应用程序返回到其原始状态。

但是，有时可能需要从备份副本还原数据集。 使用自动递增值时，可能会出现此问题的一个示例。 例如，如果保存操作不成功，则数据集中不会重置自动递增值，并且数据集将继续创建自动递增值。 这会在编号方面留下一个在应用程序中可能不可接受的空白。 如果这是一个问题，则 提供一个 属性，该属性在事务失败时将现有数据集替换为 `TableAdapterManager` `BackupDataSetBeforeUpdate` 备份副本。

> [!NOTE]
> 备份副本仅在方法运行时 `TableAdapterManager.UpdateAll` 位于内存中。 因此，无法以编程方式访问此备份数据集，因为它要么替换原始数据集，要么在方法完成运行后 `TableAdapterManager.UpdateAll` 即超出范围。

## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>修改生成的保存代码以执行分层更新

通过调用 `TableAdapterManager.UpdateAll` 方法并传入包含相关表的数据集的名称，可将数据集中相关数据表的更改保存到数据库。 例如，运行 `TableAdapterManager.UpdateAll(NorthwindDataset)` 方法将 NorthwindDataset 中所有表的更新发送到后端数据库。

从“数据源”窗口放置项后，代码会自动添加到 `Form_Load` 事件以填充每个表（`TableAdapter.Fill` 方法）。 代码还将添加到 <xref:System.Windows.Forms.BindingNavigator> 的“保存”按钮 click 事件中，以将数据集中的数据存回数据库中（`TableAdapterManager.UpdateAll` 方法）。

生成的保存代码还包含调用 `CustomersBindingSource.EndEdit` 方法的一行代码。 更具体地说，它 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用添加到窗体 <xref:System.Windows.Forms.BindingSource> 的第一个 的 方法。 换句话说，此代码仅针对从"数据源"窗口拖动到窗体上的第一个表生成。 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用将提交当前正在编辑的任何数据绑定控件中的所有更改。 因此，如果数据绑定控件仍具有焦点，则单击“保存”按钮后，会先提交该控件中所有挂起的编辑，然后再执行真正的保存（`TableAdapterManager.UpdateAll` 方法）。

> [!NOTE]
> 该 **数据集设计器** 仅添加要放到窗体 `BindingSource.EndEdit` 上的第一个表的代码。 因此，必须对窗体上的每个相关表添加一行调用 `BindingSource.EndEdit` 方法的代码。 对于本演练，这意味着你必须添加一个对 `OrdersBindingSource.EndEdit` 方法的调用。

### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>更新代码以在保存前提交对相关表的更改

1. 双击 <xref:System.Windows.Forms.BindingNavigator> 上的“保存”按钮以在代码编辑器中打开“Form1”。

2. 在调用 `OrdersBindingSource.EndEdit` 方法的代码行后添加一行调用 `CustomersBindingSource.EndEdit` 方法的代码。 “保存”按钮 click 事件中的代码应如下所示：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet1":::

除了在将数据保存到数据库之前提交对相关子表的更改外，你可能还需要在向数据集添加新子记录之前先提交新创建的父记录。 换句话说，可能需要将新的父记录 () 添加到数据集，然后外键约束才能将新的子 () 添加到 `Customer` `Orders` 数据集。 为实现这一点，可以使用子 `BindingSource.AddingNew` 事件。

> [!NOTE]
> 是否必须提交新的父记录取决于用于绑定到数据源的控件类型。 本演练使用单个控件绑定到父表。 这需要额外的代码来提交新的父记录。 如果父记录改为显示在复杂绑定控件（如 ）中，则无需对父记录进行此附加 <xref:System.Windows.Forms.DataGridView> <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用。 这是因为这类控件的基础数据绑定功能可以提交新记录。

### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>添加代码以在添加新子记录之前在数据集中提交父记录

1. 为 `OrdersBindingSource.AddingNew` 事件创建一个事件处理程序。

    - 在设计 **视图中打开 Form1，** 在组件栏中选择 **"OrdersBindingSource"，** 在"属性"窗口中选择"事件"，然后双击 **"添加""新建"** 事件。 

2. 向调用 方法的事件处理程序添加一行 `CustomersBindingSource.EndEdit` 代码。 `OrdersBindingSource_AddingNew` 事件处理程序中的代码应如下所示：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet2":::

## <a name="tableadaptermanager-reference"></a>TableAdapterManager 参考

默认情况下，创建 `TableAdapterManager` 包含相关表的数据集时，会生成类。 若要防止生成类，请将数据集的 属性的值更改为 `Hierarchical Update` false。 将具有关系的表拖动到窗体或 WPF Windows的设计图面上时，Visual Studio声明 类的成员变量。 如果不使用数据绑定，必须手动声明变量。

`TableAdapterManager`类不是 .NET 类型。 因此，你无法查看文档中的此内容。 它是在设计时作为数据集创建过程的一部分创建的。

以下是 类的常用方法和 `TableAdapterManager` 属性：

|成员|说明|
|------------|-----------------|
|`UpdateAll` 方法|保存所有数据表中的所有数据。|
|`BackUpDataSetBeforeUpdate` 属性|确定是否在执行 方法之前创建数据集的备份 `TableAdapterManager.UpdateAll` 副本。布尔。|
|*tableName* `TableAdapter` 财产|表示 `TableAdapter` 。 生成的 `TableAdapterManager` 包含它所管理的每个 `TableAdapter` 属性。 例如，使用包含 和 属性的 生成包含 Customers 和 Orders 表 `TableAdapterManager` 的 `CustomersTableAdapter` `OrdersTableAdapter` 数据集。|
|`UpdateOrder` 属性|控制单个插入、更新和删除命令的顺序。 将此选项设置为 枚举中的值 `TableAdapterManager.UpdateOrderOption` 之一。<br /><br /> 默认情况下， `UpdateOrder` 设置为 **InsertUpdateDelete**。 这意味着，对数据集中所有表执行插入、更新和删除操作。|

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
