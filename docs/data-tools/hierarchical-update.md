---
title: 分层更新
description: 查看分层更新，包括将更新后的数据（从包含 2+ 个相关表的数据集）保存回 DB，同时保留引用完整性规则。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601154"
---
# <a name="hierarchical-update"></a>分层更新

分层更新是指在维护引用完整性规则的同时将更新的数据（从包含两个或多个相关表的数据集）保存回数据库的过程。 引用完整性是指数据库中控制插入、更新和删除相关记录的行为的约束提供的一致性规则。 例如，根据引用完整性，在允许为该客户创建订单之前，应强制创建客户记录。  有关数据集中关系的详细信息，请参阅[数据集中的关系](../data-tools/relationships-in-datasets.md)。

分层更新功能使用 `TableAdapterManager` 管理类型化数据集中的 `TableAdapter`。 `TableAdapterManager` 组件是 Visual Studio 生成的类，而不是 .NET 类型。 将表从“数据源”窗口拖到 Windows 窗体或 WPF 页面时，Visual Studio 会在窗体或页面中添加类型 TableAdapterManager 的变量，且你可在组件栏的设计器中看到它。 有关 `TableAdapterManager` 类的详细信息，请参阅 [TableAdapters](../data-tools/create-and-configure-tableadapters.md) 的 TableAdapterManager 引用部分。

默认情况下，数据集将相关表视为“仅限关系”，这意味着它不会强制执行外键约束。 可以在设计时通过使用“数据集设计器”修改该设置。 选择两个表之间的关系行以打开“关系”对话框。 在此处做出的更改将决定在将相关表中的更改发送回数据库时 `TableAdapterManager` 的行为。

## <a name="enable-hierarchical-update-in-a-dataset"></a>在数据集中启用分层更新

默认情况下，为项目中添加或创建的所有新数据集启用分层更新。 通过将数据集中的类型化数据集的“分层更新”属性设置为“True”或“False”，来打开或关闭分层更新  ：

![分层更新设置](../data-tools/media/hierarchical-update-setting.png)

## <a name="create-a-new-relation-between-tables"></a>在表之间创建新关系

若要在两个表之间创建新的关系，请在数据集设计器中，选择每个表的标题栏，然后右键单击并选择“添加关系”。

![分层更新添加关系菜单](../data-tools/media/hierarchical-update-add-relation-menu.png)

## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>了解外键约束、级联更新和删除

了解如何在生成的数据集代码中创建数据库中的外键约束和级联行为非常重要。

默认情况下，数据集中的数据表生成时具有与数据库中的关系匹配的关系 (<xref:System.Data.DataRelation>)。 但是，数据集中的关系不会作为外键约束生成。 实际上，<xref:System.Data.DataRelation> 会配置为“仅限关系”，且没有 <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> 或 <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A>。

默认情况下，即使数据库关系设置为级联更新和/或级联删除打开，级联更新和级联删除也会关闭。 例如，创建新客户和新订单，然后尝试保存数据可能会导致与数据库中定义的外键约束的冲突。 有关详细信息，请参阅[在填充数据集时关闭约束](turn-off-constraints-while-filling-a-dataset.md)。

## <a name="set-the-order-to-perform-updates"></a>设置执行更新的顺序

设置执行更新的顺序设置为保存数据集所有表中所有修改数据所需的单个插入、更新和删除的顺序。 启用分层更新后，首先执行插入，然后更新，然后删除。 `TableAdapterManager` 提供了一个 `UpdateOrder` 属性，可以设置为先执行更新，然后插入，再删除。

> [!NOTE]
> 了解更新顺序包含所有内容非常重要。 即在执行更新操作时，对数据集中的所有表执行插入和删除操作。

若要设置 `UpdateOrder` 属性，在将项从[“数据源”窗口](add-new-data-sources.md#data-sources-window)到窗体上后，选择组件栏中的 `TableAdapterManager`，然后在“属性”窗口中设置 `UpdateOrder` 属性。

## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>在执行分层更新之前创建数据集的备份副本

保存数据（通过调用 `TableAdapterManager.UpdateAll()` 方法）时，`TableAdapterManager` 尝试在单个事务中更新每个表的数据。 如果任何表的更新的任何部分失败，则会回退整个事务。 在大多数情况下，回退将应用程序返回到其原始状态。

但是，有时可能需要从备份副本还原数据集。 使用自动递增值时，可能会出现此问题的一个示例。 例如，如果保存操作不成功，则数据集中不会重置自动增量值，数据集将继续创建自动增量值。 这会在编号方面留下一个在应用程序中可能不可接受的空白。 在出现此问题的情况下，`TableAdapterManager` 提供 `BackupDataSetBeforeUpdate` 属性，如果事务失败，该属性会将现有数据集替换为备份副本。

> [!NOTE]
> 备份副本仅在 `TableAdapterManager.UpdateAll` 方法运行时位于内存中。 因此，此备份数据集没有编程访问，因为它要么替换原始数据集，要么在 `TableAdapterManager.UpdateAll` 方法完成运行后超出范围。

## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>修改生成的保存代码以执行分层更新

通过调用 `TableAdapterManager.UpdateAll` 方法并传入包含相关表的数据集的名称，可将数据集中相关数据表的更改保存到数据库。 例如，运行 `TableAdapterManager.UpdateAll(NorthwindDataset)` 方法将 NorthwindDataset 中所有表的更新发送到后端数据库。

从“数据源”窗口放置项后，代码会自动添加到 `Form_Load` 事件以填充每个表（`TableAdapter.Fill` 方法）。 代码还将添加到 <xref:System.Windows.Forms.BindingNavigator> 的“保存”按钮 click 事件中，以将数据集中的数据存回数据库中（`TableAdapterManager.UpdateAll` 方法）。

生成的保存代码还包含调用 `CustomersBindingSource.EndEdit` 方法的一行代码。 更具体地说，它调用添加到窗体的第一个 <xref:System.Windows.Forms.BindingSource> 的 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 方法。 也就是说，此代码只是为从“数据源”窗口拖到窗体上的第一个表生成的。 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用将提交当前正在编辑的任何数据绑定控件中的所有更改。 因此，如果数据绑定控件仍具有焦点，则单击“保存”按钮后，会先提交该控件中所有挂起的编辑，然后再执行真正的保存（`TableAdapterManager.UpdateAll` 方法）。

> [!NOTE]
> “数据集设计器”只为放置到窗体上的第一个表添加 `BindingSource.EndEdit` 代码。 因此，必须对窗体上的每个相关表添加一行调用 `BindingSource.EndEdit` 方法的代码。 对于本演练，这意味着你必须添加一个对 `OrdersBindingSource.EndEdit` 方法的调用。

### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>更新代码以在保存前提交对相关表的更改

1. 双击 <xref:System.Windows.Forms.BindingNavigator> 上的“保存”按钮以在代码编辑器中打开“Form1”。

2. 在调用 `OrdersBindingSource.EndEdit` 方法的代码行后添加一行调用 `CustomersBindingSource.EndEdit` 方法的代码。 “保存”按钮 click 事件中的代码应如下所示：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet1":::

除了在将数据保存到数据库之前提交对相关子表的更改外，你可能还需要在向数据集添加新子记录之前先提交新创建的父记录。 也就是说，你可能需要先向数据集添加新父记录 (`Customer`)，然后外键约束才允许将新子记录 (`Orders`) 添加到数据集中。 为实现这一点，可以使用子 `BindingSource.AddingNew` 事件。

> [!NOTE]
> 你是否提交新父记录具体取决于用于绑定到数据源的控件的类型。 本演练使用个别控件绑定到父表。 这需要额外的代码来提交新的父记录。 如果父记录在类似于 <xref:System.Windows.Forms.DataGridView> 的复杂绑定控件中显示，则对该父记录的额外 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用不是必需的。 这是因为这类控件的基础数据绑定功能可以提交新记录。

### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>添加代码以在添加新子记录之前在数据集中提交父记录

1. 为 `OrdersBindingSource.AddingNew` 事件创建一个事件处理程序。

    - 在设计视图中打开“Form1”、在组件栏中选择“OrdersBindingSource”、在“属性”窗口中选择“事件”，然后双击“AddingNew”事件    。

2. 向事件处理程序添加调用 `CustomersBindingSource.EndEdit` 方法的一行代码。 `OrdersBindingSource_AddingNew` 事件处理程序中的代码应如下所示：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet2":::

## <a name="tableadaptermanager-reference"></a>TableAdapterManager 引用

默认情况下，创建包含相关表的数据集时，将生成 `TableAdapterManager` 类。 若要防止生成该类，请将数据集的 `Hierarchical Update` 属性值更改为 false。 将具有关系的表拖到 Windows 窗体或 WPF 页面的设计图面上时，Visual Studio 会声明该类的一个成员变量。 如果不使用数据绑定，则必须手动声明该变量。

此 `TableAdapterManager` 类不是 .NET 类型。 因此，无法在文档中查找它。 它是在创建数据集的过程中进行设计时创建的。

以下是 `TableAdapterManager` 类的常用方法和属性：

|成员|说明|
|------------|-----------------|
|`UpdateAll` 方法|保存所有数据表中的所有数据。|
|`BackUpDataSetBeforeUpdate` 属性|确定是否在执行 `TableAdapterManager.UpdateAll` 方法之前创建数据集的备份副本。布尔。|
|tableName `TableAdapter` 属性|表示 `TableAdapter`。 生成的 `TableAdapterManager` 包含其管理的每个 `TableAdapter` 的属性。 例如，具有 Customers 和 Orders 表的数据集将生成包含 `CustomersTableAdapter` 和 `OrdersTableAdapter` 属性的 `TableAdapterManager`。|
|`UpdateOrder` 属性|控制单个插入、更新和删除命令的顺序。 将此设置为 `TableAdapterManager.UpdateOrderOption` 枚举中的任一值。<br /><br /> 默认情况下，`UpdateOrder` 设置为 InsertUpdateDelete。 这意味着，对数据集中所有表执行插入、更新和删除操作。|

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
