---
title: 将数据保存回数据库
description: 使用数据集工具将数据保存回数据库。 数据集是数据的内存中副本，如果修改了此数据，则应将其保存回数据库。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- datasets [Visual Basic], validating data
- data validation, datasets
- data [Visual Studio], saving
- row version
- updating datasets, constraints
- datasets [Visual Basic], about datasets
- datasets [Visual Basic], merging
- updates, constraints in datasets
- saving data, about saving data
- datasets [Visual Basic], constraints
- TableAdapters
ms.assetid: afe6cb8a-dc6a-428b-b07b-903ac02c890b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 36140f928450cbb8ef498ae1edb490b4c2a32eae
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601111"
---
# <a name="save-data-back-to-the-database"></a>将数据保存回数据库

数据集是数据的内存中副本。 如果修改此数据，最好将这些更改保存回数据库。 可通过下面三种方式之一实现此目的：

- 通过调用 TableAdapter 的 `Update` 方法之一

- 通过调用 TableAdapter 的 `DBDirect` 方法之一

- 通过对 TableAdapterManager 调用 `UpdateAll` 方法；当数据集包含与数据集中的其他表相关的表时，Visual Studio 将为你生成 TableAdapterManager

通过数据绑定将数据集表绑定到 Windows 窗体或 XAML 页面上的控件时，数据绑定体系结构将为你完成所有工作。

如果熟悉 Tableadapter，可直接跳转到以下主题之一：

|主题|说明|
|-----------|-----------------|
|[将新记录插入数据库](../data-tools/insert-new-records-into-a-database.md)|如何使用 Tableadapter 或 Command 对象执行更新和插入操作|
|[使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)|如何通过 Tableadapter 执行更新|
|[分层更新](../data-tools/hierarchical-update.md)|如何从包含两个或多个相关表的数据集执行更新|
|[处理并发异常](../data-tools/handle-a-concurrency-exception.md)|在两位用户同时尝试更改数据库中的同一数据时如何处理异常|
|[如何：通过使用事务来保存数据](../data-tools/save-data-by-using-a-transaction.md)|如何使用系统在事务中保存数据。 事务命名空间和 TransactionScope 对象|
|[在事务中保存数据](../data-tools/save-data-in-a-transaction.md)|关于创建 Windows 窗体应用程序的演练，用于演示如何将数据保存到事务内的数据库中|
|[将数据保存到数据库（多个表）](../data-tools/save-data-to-a-database-multiple-tables.md)|如何编辑记录并将多个表中的更改保存回数据库|
|[将数据从对象保存到数据库](../data-tools/save-data-from-an-object-to-a-database.md)|如何使用 TableAdapter DbDirect 方法将数据从一个不在数据集中的对象传递到数据库|
|[用 TableAdapter DBDirect 方法保存数据](../data-tools/save-data-with-the-tableadapter-dbdirect-methods.md)|如何使用 TableAdapter 将 SQL 查询直接发送到数据库|
|[将数据集另存为 XML](../data-tools/save-a-dataset-as-xml.md)|如何将数据集保存到 XML 文档|

## <a name="two-stage-updates"></a>两阶段式更新

更新数据源的过程分为两个步骤。 第一步是更新包含新记录、已更改记录或已删除记录的数据集。 如果应用程序永远不会将这些更改发送回数据源，则已完成更新。

如果将更改发送回数据库，则需要执行第二步。 如果未使用数据绑定控件，必须手动调用与用于填充数据集的相同 TableAdapter（或数据适配器）的 `Update` 方法。 但也可使用其他适配器，例如，将数据从一个数据源移动到另一个数据源，或更新多个数据源。 如果不使用数据绑定，并且要保存对相关表所做的更改，必须手动实例化自动生成的 `TableAdapterManager` 类的变量，然后调用其 `UpdateAll` 方法。

![数据集更新的概念图](../data-tools/media/vbdatasetupdates.gif)

数据集包含表的集合，表则包含行的集合。 如果要在以后更新基础数据源，必须在添加或删除行时对 `DataTable.DataRowCollection` 属性使用这些方法。 这些方法会执行更新数据源所需的更改跟踪。 如果对 Rows 属性调用 `RemoveAt` 集合，则不会将删除操作传递回数据库。

## <a name="merge-datasets"></a>合并数据集

可通过将数据集与其他数据集合并来更新该数据集的内容。 此方法涉及将源数据集的内容复制到调用数据集（称为目标数据集） 。 合并数据集时，会将源数据集中的新记录添加到目标数据集。 此外，还会将源数据集中的额外列添加到目标数据集。 如果有本地数据集，并且从另一个应用程序获得第二个数据集，则合并数据集会很有用。 在从组件（例如 XML Web 服务）获取第二个数据集时，或者在需要集成多个数据集的数据时，这也很有用。

合并数据集时，可传递布尔参数 (`preserveChanges`)，该参数指出 <xref:System.Data.DataSet.Merge%2A> 方法是否保留目标数据集中的现有修改。 数据集会维护多个版本的记录，因此请务必记住合并的是多个版本的记录。 下表显示了如何合并两个数据集中的记录：

|DataRowVersion|目标数据集|源数据集|
| - | - | - |
|原始|James Wilson|James C. Wilson|
|当前|Jim Wilson|James C. Wilson|

如果使用 `preserveChanges=false targetDataset.Merge(sourceDataset)` 对上表调用 <xref:System.Data.DataSet.Merge%2A> 方法，会得到以下数据：

|DataRowVersion|目标数据集|源数据集|
| - | - | - |
|原始|James C. Wilson|James C. Wilson|
|当前|James C. Wilson|James C. Wilson|

如果使用 `preserveChanges = true targetDataset.Merge(sourceDataset, true)` 调用 <xref:System.Data.DataSet.Merge%2A> 方法，会得到以下数据：

|DataRowVersion|目标数据集|源数据集|
| - | - | - |
|原始|James C. Wilson|James C. Wilson|
|当前|Jim Wilson|James C. Wilson|

> [!CAUTION]
> 在 `preserveChanges = true` 方案中，如果对目标数据集中的记录调用 <xref:System.Data.DataSet.RejectChanges%2A> 方法，则它将还原为源数据集中的原始数据。 这意味着，如果尝试用目标数据集更新原始数据源，则可能找不到要更新的原始行。 防止并发冲突的方法：使用数据源中已更新的记录填充另一个数据集，然后执行合并来防止发生并发冲突。 （在填充数据集后，另一位用户修改数据源中的记录时，会发生并发冲突。）

## <a name="update-constraints"></a>更新约束

若要更改现有数据行，请在单独的列中添加或更新数据。 如果数据集包含约束（例如外键或不可为 null 的约束），则在更新记录时，它可能会暂时处于错误状态。 也就是说，在完成一列的更新之后和到达下一列前之间，它可能处于错误状态。

若要防止过早违反约束，可暂时暂停更新约束。 这有两种用途：

- 防止在完成更新一列但尚未开始更新其他列时引发错误。

- 防止引发某些更新事件（通常用于验证的事件）。

> [!NOTE]
> 在 Windows 窗体中，datagrid 中内置的数据绑定体系结构会暂停约束检查，直到焦点移出行为止，并且你无需显式调用 <xref:System.Data.DataRow.BeginEdit%2A>、<xref:System.Data.DataRow.EndEdit%2A> 或 <xref:System.Data.DataRow.CancelEdit%2A> 方法。

对数据集调用 <xref:System.Data.DataSet.Merge%2A> 方法时，会自动禁用约束。 合并完成后，如果数据集上有任何无法启用的约束，会引发 <xref:System.Data.ConstraintException>。 在这种情况下，<xref:System.Data.DataSet.EnforceConstraints%2A> 属性被设置为 `false,`，并且必须在将 <xref:System.Data.DataSet.EnforceConstraints%2A> 属性重置为 `true` 之前解决所有约束冲突。

完成更新后，可重启约束检查，这也会重启更新事件并引发这些事件。

有关挂起事件的详细信息，请参阅[在填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

## <a name="dataset-update-errors"></a>数据集更新错误

更新数据集中的记录时，可能会出错。 例如，可能会无意中将错误类型的数据写入列、写入过长的数据或具有其他完整性问题的数据。 或者，你可能具有特定于应用程序的验证检查，这些检查可能在更新事件的任何阶段引发自定义错误。 有关详细信息，请参阅[验证数据集中的数据](../data-tools/validate-data-in-datasets.md)。

## <a name="maintain-information-about-changes"></a>维护有关更改的信息

数据集中更改的相关信息是通过两种方式维护的：第一种方式是标记行来表示它们已更改 (<xref:System.Data.DataRow.RowState%2A>)；第二种方式是保留记录的多个副本 (<xref:System.Data.DataRowVersion>)。 通过使用此信息，进程可确定数据集中已更改的内容，并可将适当的更新发送到数据源。

### <a name="rowstate-property"></a>RowState 属性

<xref:System.Data.DataRow> 对象的 <xref:System.Data.DataRow.RowState%2A> 属性是一个值，它提供特定数据行的状态的相关信息。

下表详细描述了 <xref:System.Data.DataRowState> 枚举的可能值：

|DataRowState 值|说明|
| - |-----------------|
|<xref:System.Data.DataRowState.Added>|该行已作为项添加到 <xref:System.Data.DataRowCollection>。 （处于此状态的行没有相应的原始版本，因为它在调用最后一个 <xref:System.Data.DataRow.AcceptChanges%2A> 方法时不存在）。|
|<xref:System.Data.DataRowState.Deleted>|该行是使用 <xref:System.Data.DataRow> 对象的 <xref:System.Data.DataRow.Delete%2A> 删除的。|
|<xref:System.Data.DataRowState.Detached>|已创建该行，但它不是任何 <xref:System.Data.DataRowCollection> 的一部分。 <xref:System.Data.DataRow> 对象在创建后、添加到集合之前以及从集合中删除之后，会立即进入此状态。|
|<xref:System.Data.DataRowState.Modified>|行中的列值已发生某种更改。|
|<xref:System.Data.DataRowState.Unchanged>|自上一次调用 <xref:System.Data.DataRow.AcceptChanges%2A> 之后，该行未更改。|

### <a name="datarowversion-enumeration"></a>DataRowVersion 枚举

数据集会维护多个版本的记录。 在使用 <xref:System.Data.DataRow> 对象的 <xref:System.Data.DataRow.Item%2A> 属性或 <xref:System.Data.DataRow.GetChildRows%2A> 方法检索在 <xref:System.Data.DataRow> 中发现的值时，会使用 <xref:System.Data.DataRowVersion> 字段。

下表详细描述了 <xref:System.Data.DataRowVersion> 枚举的可能值：

|DataRowVersion 值|说明|
| - |-----------------|
|<xref:System.Data.DataRowVersion.Current>|记录的当前版本包含自上次调用 <xref:System.Data.DataRow.AcceptChanges%2A> 以来对记录执行的所有修改。 如果该行已删除，则没有当前版本。|
|<xref:System.Data.DataRowVersion.Default>|由数据集架构或数据源定义的记录的默认值。|
|<xref:System.Data.DataRowVersion.Original>|记录的原始版本是在数据集中最后一次提交更改时记录的副本。 实际上，这通常是从数据源读取的记录版本。|
|<xref:System.Data.DataRowVersion.Proposed>|在更新期间（即调用 <xref:System.Data.DataRow.BeginEdit%2A> 方法与 <xref:System.Data.DataRow.EndEdit%2A> 方法之间）暂时可用的记录的建议版本。 通常在事件（如 <xref:System.Data.DataTable.RowChanging>）的处理程序中访问记录的建议版本。 调用 <xref:System.Data.DataRow.CancelEdit%2A> 方法会反转更改并删除数据行的建议版本。|

将更新信息传输到数据源时，原始版本和当前版本非常有用。 通常，将更新发送到数据源时，数据库的新信息位于记录的当前版本中。 原始版本中的信息用于查找要更新的记录。

例如，如果更改了记录的主键，则需要通过某种方法在数据源中查找正确的记录，以便更新更改。 如果不存在原始版本，则很可能会将记录追加到数据源，这不仅会导致产生额外的多余记录，还会导致一条记录不准确且过期。 这两个版本也用于并发控制。 可将原始版本与数据源中的记录进行比较，确定记录在加载到数据集后是否出现了更改。

在实际将更改提交到数据集之前需要执行验证，此时建议的版本非常有用。

即使记录已更改，也并不总是有该行的原始版本或当前版本。 在表中插入新行时，没有原始版本，只有当前版本。 同样，如果通过调用表的 `Delete` 方法删除行，则存在原始版本，但没有当前版本。

可通过查询数据行的 <xref:System.Data.DataRow.HasVersion%2A> 方法进行测试，以查看是否存在特定版本的记录。 请求列的值时，可通过将 <xref:System.Data.DataRowVersion> 枚举值作为可选参数传递来访问记录的任一版本。

## <a name="get-changed-records"></a>获取已更改的记录

通常不会更新数据集中的每个记录。 例如，用户可能正在使用一个显示许多记录的 Windows 窗体 <xref:System.Windows.Forms.DataGridView> 控件。 但是该用户可能只更新一些记录、删除一条记录并插入一个新记录。 数据集和数据表提供了一种方法 (`GetChanges`)，可仅返回已修改的行。

可使用数据表 (<xref:System.Data.DataTable.GetChanges%2A>) 或数据集 (<xref:System.Data.DataSet.GetChanges%2A>) 本身的 `GetChanges` 方法创建已更改的记录的子集。 如果为数据表调用该方法，将返回仅包含已更改记录的表副本。 同样，如果对数据集调用该方法，会获得仅包含已更改记录的新数据集。

`GetChanges` 本身会返回所有已更改的记录。 相反，通过将所需的 <xref:System.Data.DataRowState> 作为参数传递给 `GetChanges` 方法，可指定所需的已更改记录的子集，其中包括：新添加的记录、标记为要删除的记录、拆离的记录或已修改的记录。

在将记录发送到另一个组件进行处理时，获取已更改记录的子集会很有帮助。 可通过仅获取组件所需的记录来减少与其他组件通信的开销，而不是发送整个数据集。

## <a name="commit-changes-in-the-dataset"></a>提交数据集中的更改

在数据集中进行更改时，将设置已更改行的 <xref:System.Data.DataRow.RowState%2A> 属性。 系统会建立和维护记录的原始版本和当前版本，并通过 <xref:System.Data.DataRowView.RowVersion%2A> 属性提供这些版本。 若要向数据源发送正确更新，必须使用存储在这些已更改行的属性中的元数据。

如果更改反映了数据源的当前状态，则不再需要维护此信息。 通常，数据集及其数据源有两次同步的情况：

- 在将信息加载到数据集之后（例如从数据源读取数据时）会立刻同步。

- 在将更改从数据集发送到数据源之后（但不是在此之前，在之前同步会使你丢失将更改发送到数据库所需的更改信息）会同步。

可调用 <xref:System.Data.DataSet.AcceptChanges%2A> 方法将挂起的更改提交到数据集。 通常会在下列时间调用 <xref:System.Data.DataSet.AcceptChanges%2A>：

- 加载数据集后。 如果通过调用 TableAdapter 的 `Fill` 方法加载数据集，则适配器会自动提交更改。 但是，如果通过将另一个数据集合并到数据集中来加载数据集，则必须手动提交更改。

    > [!NOTE]
    > 可通过将适配器的 `AcceptChangesDuringFill` 属性设置为 `false`，阻止适配器在调用 `Fill` 方法时自动提交更改。 如果设置为 `false`，则会将填充期间插入的每一行的 <xref:System.Data.DataRow.RowState%2A> 都设置为 <xref:System.Data.DataRowState.Added>。

- 将数据集更改发送到另一个进程（如 XML Web 服务）之后。

    > [!CAUTION]
    > 这样提交更改会清除所有更改信息。 在执行要求应用程序知道数据集中进行了哪些更改的操作之前，请勿提交更改。

此方法可实现以下目的：

- 将记录的 <xref:System.Data.DataRowVersion.Current> 版本写入其 <xref:System.Data.DataRowVersion.Original> 版本并覆盖原始版本。

- 删除 <xref:System.Data.DataRow.RowState%2A> 属性设置为 <xref:System.Data.DataRowState.Deleted> 的所有行。

- 将记录的 <xref:System.Data.DataRow.RowState%2A> 属性设置为 <xref:System.Data.DataRowState.Unchanged>。

<xref:System.Data.DataSet.AcceptChanges%2A> 方法在 3 个级别可用。 可在 <xref:System.Data.DataRow> 对象上调用该方法，仅提交该行的更改。 还可在 <xref:System.Data.DataTable> 对象上调用该方法来提交表中的所有行。 最后，可在 <xref:System.Data.DataSet> 对象上调用该方法，以提交数据集所有表的所有记录中所有挂起的更改。

下表描述了基于调用方法的对象提交哪些更改：

|方法|结果|
|------------|------------|
|<xref:System.Data.DataRow.AcceptChanges%2A?displayProperty=fullName>|仅提交特定行上的更改。|
|<xref:System.Data.DataTable.AcceptChanges%2A?displayProperty=fullName>|提交特定表中所有行上的更改。|
|<xref:System.Data.DataSet.AcceptChanges%2A?displayProperty=fullName>|提交数据集的所有表的所有行上的更改。|

> [!NOTE]
> 如果通过调用 TableAdapter 的 `Fill` 方法加载数据集，则不需要显式接受更改。 默认情况下，`Fill` 方法在填充完数据表后会调用 `AcceptChanges` 方法。

<xref:System.Data.DataSet.RejectChanges%2A> 是一个相关方法，该方法将记录的 <xref:System.Data.DataRowVersion.Original> 版本复制回 <xref:System.Data.DataRowVersion.Current> 版本，从而达到撤消更改的效果。 它还将每个记录的 <xref:System.Data.DataRow.RowState%2A> 设置回 <xref:System.Data.DataRowState.Unchanged>。

## <a name="data-validation"></a>数据验证

为了验证应用程序中的数据是否满足其传递到的进程的要求，通常必须添加验证。 这可能涉及到检查用户在窗体中输入的内容是否正确，验证其他应用程序发送给应用程序的数据，甚至可能要检查在组件中计算的信息是否在数据源和应用程序要求的约束范围内。

可通过多种方式验证数据：

- 在业务层中，通过将代码添加到应用程序来验证数据。 可在数据集中执行此操作。 数据集提供后端验证的一些优点，例如，能够在更改列和行值时验证更改。 有关详细信息，请参阅[验证数据集中的数据](../data-tools/validate-data-in-datasets.md)。

- 在表示层中，方法是向窗体添加验证。 有关详细信息，请参阅 [Windows 窗体中的用户输入验证](/dotnet/framework/winforms/user-input-validation-in-windows-forms)。

- 在数据后端，方法是将数据发送到数据源（例如数据库），并允许数据源接受或拒绝数据。 如果使用的数据库具有用于验证数据和提供错误信息的复杂实施，则这可能是一种可行的方法，因为无论数据来自何处，都可以验证数据。 但是，这种方法可能无法满足特定于应用程序的验证要求。 此外，使数据源验证数据可能会导致到数据源的大量往返，具体取决于应用程序如何帮助解决后端引发的验证错误。

   > [!IMPORTANT]
   > 当使用 <xref:System.Data.SqlClient.SqlCommand.CommandType%2A> 属性设置为 <xref:System.Data.CommandType.Text> 的数据命令时，请先仔细检查从客户端发送的信息，再将其传递至数据库。 恶意用户会设法发送（注入）经过修改或附加的 SQL 语句，企图对数据库进行未经授权的访问或破坏数据库。 在将用户输入传输到数据库之前，始终要验证信息是否有效。 最佳做法是尽可能使用参数化查询或存储过程。

## <a name="transmit-updates-to-the-data-source"></a>将更新传输到数据源

在数据集中进行更改后，可以将这些更改传输到数据源。 最常见的情况是通过调用 TableAdapter（或数据适配器）的 `Update` 方法来执行此操作。 该方法会循环遍历数据表中的每个记录，确定需要哪种类型的更新（更新、插入或删除）（如果有），然后运行相应的命令。

为了说明如何进行更新，此处假设应用程序使用包含单个数据表的数据集。 应用程序从数据库中提取两行。 检索完成后，内存中数据表如下所示：

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Unchanged)    c400         Nancy Buchanan    Pending
```

应用程序将 Nancy Buchanan 的状态更改为“首选”。 由于此更改，该行的 <xref:System.Data.DataRow.RowState%2A> 属性的值从 <xref:System.Data.DataRowState.Unchanged> 更改为 <xref:System.Data.DataRowState.Modified>。 第一行的 <xref:System.Data.DataRow.RowState%2A> 属性的值将保持为 <xref:System.Data.DataRowState.Unchanged>。 数据表现在如下所示：

```sql
(RowState)     CustomerID   Name             Status
(Unchanged)    c200         Robert Lyon      Good
(Modified)     c400         Nancy Buchanan    Preferred
```

应用程序现在调用 `Update` 方法，将数据集传送给数据库。 该方法会依次检查每一行。 对于第一行，该方法不会向数据库传输 SQL 语句，原因是自最初从数据库提取该行以来，该行未发生更改。

但对于第二行，`Update` 方法会自动调用正确的数据命令并将其传输到数据库。 SQL 语句的特定语法取决于基础数据存储所支持的 SQL 方言。 但是，值得注意已传输的 SQL 语句的下列一般特征：

- 传输的 SQL 语句是一个 UPDATE 语句。 适配器知道要使用 UPDATE 语句，因为 <xref:System.Data.DataRow.RowState%2A> 属性的值为 <xref:System.Data.DataRowState.Modified>。

- 传输的 SQL 语句包含一个 WHERE 子句，它指示 UPDATE 语句的目标为 `CustomerID = 'c400'` 的行。 SELECT 语句的此部分将目标行与所有其他行区分开来，因为 `CustomerID` 是目标表的主键。 WHERE 子句的信息派生自记录的原始版本 (`DataRowVersion.Original`)，以防标识行所需的值发生了更改。

- 传输的 SQL 语句包含 SET 子句，用于设置已修改列的新值。

   > [!NOTE]
   > 如果 TableAdapter 的 `UpdateCommand` 属性已设置为存储过程的名称，则该适配器将不会构造 SQL 语句。 相反，它会使用传入的相应参数调用存储过程。

## <a name="pass-parameters"></a>传递参数

通常使用参数来传递要在数据库中更新的记录的值。 当 TableAdapter 的 `Update` 方法运行 UPDATE 语句时，它需要填写参数值。 它从相应的数据命令（在本例中为 TableAdapter 中的 `UpdateCommand` 对象）的 `Parameters` 集合中获取这些值。

如果已使用 Visual Studio 工具生成数据适配器，则 `UpdateCommand` 对象将包含与语句中的每个参数占位符对应的参数集合。

每个参数的 <xref:System.Data.SqlClient.SqlParameter.SourceColumn%2A?displayProperty=fullName> 属性都指向数据表中的某一列。 例如，`au_id` 和 `Original_au_id` 参数的 `SourceColumn` 属性设置为数据表中包含作者 ID 的任何列。当适配器的 `Update` 方法运行时，它将从要更新的记录中读取作者 ID 列，并将该值填充到语句中。

在 UPDATE 语句中，需要指定新值（要写入记录的值）以及旧值（以便在数据库中找到该记录）。 因此，每个值都有两个参数：一个用于 SET 子句，另一个用于 WHERE 子句。 这两个参数都从要更新的记录中读取数据，但它们根据参数的 <xref:System.Data.SqlClient.SqlParameter.SourceVersion> 属性获取不同版本的列值。 SET 子句的参数获取当前版本，WHERE 子句的参数则获取原始版本。

> [!NOTE]
> 还可在代码中自行设置 `Parameters` 集合中的值，一般是在数据适配器的 <xref:System.Data.DataTable.RowChanging> 事件的事件处理程序中执行此操作。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [创建和配置 TableAdapter](create-and-configure-tableadapters.md)
- [使用 TableAdapter 更新数据](../data-tools/update-data-by-using-a-tableadapter.md)
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [验证数据](validate-data-in-datasets.md)
- [如何：添加、修改和删除实体（WCF 数据服务）](/dotnet/framework/data/wcf/how-to-add-modify-and-delete-entities-wcf-data-services)
