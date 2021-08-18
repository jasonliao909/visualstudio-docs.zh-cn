---
title: 分层更新
description: 查看分层更新，其中包括将已更新的数据从具有2个相关表的数据集中 () 返回到数据库，同时保留引用完整性规则。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122121989"
---
# <a name="hierarchical-update"></a>分层更新

*分层更新* 是指将已更新的数据从包含两个或多个相关) 表的数据集中 (保存到数据库中，同时保持引用完整性规则的过程。 *引用完整性* 是指数据库中约束提供的一致性规则，这些规则控制插入、更新和删除相关记录的行为。 例如，它是在允许为该客户创建订单之前强制创建客户记录的引用完整性。  有关数据集中的关系的详细信息，请参阅 [数据集中的关系](../data-tools/relationships-in-datasets.md)。

分层更新功能使用 `TableAdapterManager` 管理 `TableAdapter` 类型化数据集中的。 `TableAdapterManager`组件是 Visual Studio 生成的类，而不是 .net 类型。 将表从 "**数据源**" 窗口拖动到 Windows 窗体或 WPF 页时，Visual Studio 会将类型 TableAdapterManager 的变量添加到窗体或页中，并在组件栏的设计器中看到它。 有关类的详细信息 `TableAdapterManager` ，请参阅 [Tableadapter](../data-tools/create-and-configure-tableadapters.md)的 TableAdapterManager 参考部分。

默认情况下，数据集将相关表视为 "仅关系"，这意味着它不强制外键约束。 您可以使用 **数据集设计器** 在设计时修改该设置。 选择两个表之间的关系线，以打开 " **关系** " 对话框。 您在此处进行的更改将确定在将 `TableAdapterManager` 相关表中的更改发送回数据库时的行为方式。

## <a name="enable-hierarchical-update-in-a-dataset"></a>在数据集中启用分层更新

默认情况下，将为在项目中添加或创建的所有新数据集启用分层更新。 通过将数据集中的类型化数据集的 " **分层更新** " 属性设置为 " **True** " 或 " **False**"，打开或关闭层次结构更新：

![分层更新设置](../data-tools/media/hierarchical-update-setting.png)

## <a name="create-a-new-relation-between-tables"></a>在表之间创建新关系

若要在两个表之间创建新关系，请在数据集设计器中选择每个表的标题栏，然后右键单击并选择 " **添加关系**"。

![分层更新添加关系菜单](../data-tools/media/hierarchical-update-add-relation-menu.png)

## <a name="understand-foreign-key-constraints-cascading-updates-and-deletes"></a>了解外键约束、级联更新和删除

了解如何在生成的数据集代码中创建数据库中的外键约束和级联行为非常重要。

默认情况下，将使用与 <xref:System.Data.DataRelation> 数据库中的关系 () 关系生成数据集中的数据表。 但是，数据集中的关系不会生成为外键约束。 <xref:System.Data.DataRelation>仅当没有或不有效时，才配置为 **关系** <xref:System.Data.ForeignKeyConstraint.UpdateRule%2A> <xref:System.Data.ForeignKeyConstraint.DeleteRule%2A> 。

默认情况下，即使在启用了级联更新和/或级联删除功能的情况下，也会关闭级联更新和级联删除。 例如，创建新的客户和新订单，然后尝试保存数据会导致与数据库中定义的外键约束冲突。 有关详细信息，请参阅 [在填充数据集时关闭约束](turn-off-constraints-while-filling-a-dataset.md)。

## <a name="set-the-order-to-perform-updates"></a>设置执行更新的顺序

如果将顺序设置为 "执行更新"，则会设置在数据集的所有表中保存所有已修改数据所需的单个插入、更新和删除操作的顺序。 启用分层更新后，先执行插入，然后更新，然后删除。 `TableAdapterManager`提供一个 `UpdateOrder` 属性，该属性可以设置为先执行更新，然后再进行插入然后删除。

> [!NOTE]
> 必须了解更新顺序全部包括在内。 也就是说，在执行更新时，将对数据集中的所有表执行 insert 和 delete 操作。

若要设置 `UpdateOrder` 属性，请在将项从 " [数据源" 窗口](add-new-data-sources.md#data-sources-window) 拖到窗体上后，选择组件栏中的，然后在 `TableAdapterManager` `UpdateOrder` " **属性** " 窗口中设置属性。

## <a name="create-a-backup-copy-of-a-dataset-before-performing-a-hierarchical-update"></a>在执行分层更新之前创建数据集的备份副本

通过调用方法) 保存数据 (时 `TableAdapterManager.UpdateAll()` ， `TableAdapterManager` 会尝试在单个事务中更新每个表的数据。 如果任何表的更新的任何部分失败，则将回滚整个事务。 在大多数情况下，回滚会将您的应用程序恢复到其原始状态。

但是，有时您可能想要从备份副本还原数据集。 在使用自动增量值时，可能会出现这种情况。 例如，如果保存操作不成功，则不会在数据集中重置自动增量值，并且数据集将继续创建自动递增的值。 这会使你的应用程序中可能无法接受的编号保持空白。 如果出现这种情况，则会 `TableAdapterManager` 提供一个 `BackupDataSetBeforeUpdate` 属性，当事务失败时，将使用备份副本替换现有数据集。

> [!NOTE]
> 备份副本仅在方法运行时在内存中 `TableAdapterManager.UpdateAll` 。 因此，不能以编程方式访问此备份数据集，因为它会在方法完成运行后立即替换原始数据集或超出范围 `TableAdapterManager.UpdateAll` 。

## <a name="modify-the-generated-save-code-to-perform-the-hierarchical-update"></a>修改生成的保存代码以执行分层更新

通过调用 `TableAdapterManager.UpdateAll` 方法并传入包含相关表的数据集的名称，可将数据集中相关数据表的更改保存到数据库。 例如，运行 `TableAdapterManager.UpdateAll(NorthwindDataset)` 方法将 NorthwindDataset 中所有表的更新发送到后端数据库。

从“数据源”窗口放置项后，代码会自动添加到 `Form_Load` 事件以填充每个表（`TableAdapter.Fill` 方法）。 代码还将添加到 <xref:System.Windows.Forms.BindingNavigator> 的“保存”按钮 click 事件中，以将数据集中的数据存回数据库中（`TableAdapterManager.UpdateAll` 方法）。

生成的保存代码还包含调用 `CustomersBindingSource.EndEdit` 方法的一行代码。 更具体地讲，它调用 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> <xref:System.Windows.Forms.BindingSource> 添加到窗体中的第一个方法。 换言之，仅为从 " **数据源** " 窗口拖到窗体上的第一个表生成此代码。 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用将提交当前正在编辑的任何数据绑定控件中的所有更改。 因此，如果数据绑定控件仍具有焦点，则单击“保存”按钮后，会先提交该控件中所有挂起的编辑，然后再执行真正的保存（`TableAdapterManager.UpdateAll` 方法）。

> [!NOTE]
> **数据集设计器** 仅为拖放 `BindingSource.EndEdit` 到窗体上的第一个表添加代码。 因此，必须对窗体上的每个相关表添加一行调用 `BindingSource.EndEdit` 方法的代码。 对于本演练，这意味着你必须添加一个对 `OrdersBindingSource.EndEdit` 方法的调用。

### <a name="to-update-the-code-to-commit-changes-to-the-related-tables-before-saving"></a>更新代码以在保存前提交对相关表的更改

1. 双击 <xref:System.Windows.Forms.BindingNavigator> 上的“保存”按钮以在代码编辑器中打开“Form1”。

2. 在调用 `OrdersBindingSource.EndEdit` 方法的代码行后添加一行调用 `CustomersBindingSource.EndEdit` 方法的代码。 “保存”按钮 click 事件中的代码应如下所示：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet1":::

除了在将数据保存到数据库之前提交对相关子表的更改外，你可能还需要在向数据集添加新子记录之前先提交新创建的父记录。 换言之，您可能必须在 `Customer` 外键约束启用新的子记录 (`Orders`) 添加到数据集之前，向数据集添加新的父记录 () 。 为实现这一点，可以使用子 `BindingSource.AddingNew` 事件。

> [!NOTE]
> 是否必须提交新的父记录取决于用于绑定到数据源的控件类型。 在本演练中，您将使用各个控件绑定到父表。 这需要额外的代码来提交新的父记录。 如果父记录在复杂绑定控件（如）中显示，则 <xref:System.Windows.Forms.DataGridView> <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 不需要对父记录进行此额外调用。 这是因为这类控件的基础数据绑定功能可以提交新记录。

### <a name="to-add-code-to-commit-parent-records-in-the-dataset-before-adding-new-child-records"></a>添加代码以在添加新子记录之前在数据集中提交父记录

1. 为 `OrdersBindingSource.AddingNew` 事件创建一个事件处理程序。

    - 在 "设计" 视图中打开 " **Form1** "，在组件栏中选择 " **OrdersBindingSource** "，在 "**属性**" 窗口中选择 "**事件**"，然后双击 " **system.windows.forms.bindingsource.addingnew>** " 事件。

2. 向调用方法的事件处理程序添加一行代码 `CustomersBindingSource.EndEdit` 。 `OrdersBindingSource_AddingNew` 事件处理程序中的代码应如下所示：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/VB/Form1.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasHierarchicalUpdate/CS/Form1.cs" id="Snippet2":::

## <a name="tableadaptermanager-reference"></a>TableAdapterManager 引用

默认情况下， `TableAdapterManager` 当您创建包含相关表的数据集时，将生成一个类。 若要防止生成类，请将 `Hierarchical Update` 数据集的属性值更改为 false。 将具有关系的表拖到 Windows 窗体或 WPF 页的设计图面上时，Visual Studio 声明类的成员变量。 如果不使用数据绑定，则必须手动声明该变量。

此 `TableAdapterManager` 类不是 .net 类型。 因此，您不能在文档中查找它。 它在设计时创建，作为数据集创建过程的一部分。

下面是类的常用方法和属性 `TableAdapterManager` ：

|成员|说明|
|------------|-----------------|
|`UpdateAll` 方法|保存所有数据表中的所有数据。|
|`BackUpDataSetBeforeUpdate` 属性|确定在执行方法之前是否创建数据集的备份副本 `TableAdapterManager.UpdateAll` 。变量.|
|*tableName* `TableAdapter` 知识产权|表示 `TableAdapter` 。 生成的 `TableAdapterManager` 包含它管理的每个的属性 `TableAdapter` 。 例如，具有 Customers 和 Orders 表的数据集使用 `TableAdapterManager` 包含 `CustomersTableAdapter` 和属性的生成 `OrdersTableAdapter` 。|
|`UpdateOrder` 属性|控制单个 insert、update 和 delete 命令的顺序。 将此项设置为枚举中的值之一 `TableAdapterManager.UpdateOrderOption` 。<br /><br /> 默认情况下， `UpdateOrder` 设置为 **InsertUpdateDelete**。 这意味着，对数据集中所有表执行插入、更新和删除操作。|

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
