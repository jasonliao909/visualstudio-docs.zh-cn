---
title: 数据绑定自定义对象
description: 将对象绑定为 Visual Studio 中的数据源。 使用设计时工具将自定义对象用作应用程序中的数据源。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], object binding
- data [Visual Studio], binding to objects
- object binding
- binding, to objects
ms.assetid: ed743ce6-73af-45e5-a8ff-045eddaccc86
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: b837cf77103efa7cf07bdc6f32aabb5028670638
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601227"
---
# <a name="bind-objects-as-data-sources-in-visual-studio"></a>将对象绑定为 Visual Studio 中的数据源

Visual Studio 提供设计时工具以将自定义对象用作应用程序中的数据源。 若要将数据库中的数据存储在与 UI 控件绑定的对象中，建议的方法是使用实体框架生成类。 实体框架自动生成所有样本更改跟踪代码，这意味着当你在 DbSet 对象上调用 AcceptChanges 时，对本地对象的任何更改都会自动持续到数据库中。 有关详细信息，请参阅[实体框架文档](https://ef.readthedocs.org/en/latest/)。

> [!TIP]
> 只有在应用程序已经基于数据集的情况下，才应考虑本文中对象绑定的方法。 如果你已熟悉数据集，将要处理的数据是表格数据，且不会太复杂或太大，则也可以使用这些方法。 有关更简单的示例，涉及使用 DataReader 将数据直接加载到对象中，以及手动更新 UI 而不进行数据绑定，请参阅[使用 ADO.NET 创建简单的数据应用程序](../data-tools/create-a-simple-data-application-by-using-adonet.md)。

## <a name="object-requirements"></a>对象要求

自定义对象与 Visual Studio 中的数据设计工具配合使用的唯一要求是对象至少需要一个公共属性。

通常，自定义对象不需要任何特定的接口、构造函数或属性来充当应用程序的数据源。 但是，如果要将对象从“数据源”窗口拖动到设计图面以创建数据绑定控件，并且如果对象实现 <xref:System.ComponentModel.ITypedList> 或 <xref:System.ComponentModel.IListSource> 接口，则对象必须具有默认构造函数。 否则，Visual Studio 无法对数据源对象进行实例化，并且当你将项目拖到设计图面时，它会显示错误。

## <a name="examples-of-using-custom-objects-as-data-sources"></a>将自定义对象用作数据源的示例

虽然在将对象用作数据源时有无数方法可以实现应用程序逻辑，但对于 SQL 数据库，有几个标准操作可以通过使用 Visual Studio 生成的 TableAdapter 对象进行简化。 本页说明如何使用 TableAdapter 实现这些标准进程。 它并不用作创建自定义对象的指南。 例如，无论对象的具体实现或应用程序的逻辑如何，你通常都会执行以下标准操作：

- 将数据加载到对象（通常从数据库数据库）。

- 创建对象的类型集合。

- 向集合添加对象以及从集合中删除对象。

- 在窗体上向用户显示对象数据。

- 更改/编辑对象中的数据。

- 将数据从对象保存回数据库。

### <a name="load-data-into-objects"></a>将数据加载到对象中

对于此示例，使用 TableAdapter 将数据加载到对象中。 默认情况下，使用两种从数据库获取数据并填充数据表的方法创建 TableAdapter。

- `TableAdapter.Fill` 方法使用返回的数据填充现有数据表。

- `TableAdapter.GetData` 方法返回填充了数据的新数据表。

使用数据加载自定义对象的最简单方法是调用 `TableAdapter.GetData` 方法，循环访问返回的数据表中的行集合，并使用每行中的值填充每个对象。 可以创建一个 `GetData` 方法，为添加到 TableAdapter 的任何查询返回填充的数据表。

> [!NOTE]
> Visual Studio 默认情况下将 TableAdapter 查询命名为 `Fill` 和 `GetData`，但你可以将这些名称更改为任何有效的方法名称。

以下示例演示如何循环访问数据表中的行，并使用数据填充对象：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Form1.cs" id="Snippet4":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Form1.vb" id="Snippet4":::

### <a name="create-a-typed-collection-of-objects"></a>创建对象的类型集合

你可以为对象创建集合类，或使用 [BindingSource 组件](/dotnet/framework/winforms/controls/bindingsource-component)自动提供的类型集合。

为对象创建自定义集合类时，建议从 <xref:System.ComponentModel.BindingList%601> 继承。 此泛型类提供管理集合的功能，以及引发事件的功能，这些事件将通知发送到 Windows 窗体中的数据绑定基础结构。

<xref:System.Windows.Forms.BindingSource> 中自动生成的集合使用 <xref:System.ComponentModel.BindingList%601> 作为其类型集合。 如果应用程序不需要其他功能，则你可以在 <xref:System.Windows.Forms.BindingSource> 中维护集合。 有关详细信息，请参阅 <xref:System.Windows.Forms.BindingSource> 类的 <xref:System.Windows.Forms.BindingSource.List%2A> 属性。

> [!NOTE]
> 如果集合需要 <xref:System.ComponentModel.BindingList%601> 的基础实现未提供的功能，则应创建自定义集合，以便根据需要添加到类。

以下代码演示如何为 `Order` 对象的强类型集合创建类：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet8":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet8":::

### <a name="add-objects-to-a-collection"></a>向集合添加对象

通过调用自定义集合类或 <xref:System.Windows.Forms.BindingSource> 的 `Add` 方法将对象添加到集合中。

> [!NOTE]
> 从 <xref:System.ComponentModel.BindingList%601> 继承时，会自动为自定义集合提供 `Add`方法。

以下代码演示如何将对象添加到 <xref:System.Windows.Forms.BindingSource> 中的类型集合：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet5":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet5":::

以下代码演示如何将对象添加到从 <xref:System.ComponentModel.BindingList%601> 继承的类型集合：

> [!NOTE]
> 在此示例中，`Orders` 集合是 `Customer` 对象的属性。

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet6":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet6":::

### <a name="remove-objects-from-a-collection"></a>从集合中删除对象

通过调用自定义收集类或 <xref:System.Windows.Forms.BindingSource> 的 `Remove` 或 `RemoveAt` 方法，从集合中删除对象。

> [!NOTE]
> 从 <xref:System.ComponentModel.BindingList%601> 继承时，会自动为自定义集合提供 `Remove` 和 `RemoveAt` 方法。

下列代码显示了如何使用 <xref:System.Windows.Forms.BindingSource.RemoveAt%2A> 方法在 <xref:System.Windows.Forms.BindingSource> 中定位和删除类型集合中的对象：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataConnecting/CS/Class1.cs" id="Snippet7":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataConnecting/VB/Class1.vb" id="Snippet7":::

### <a name="display-object-data-to-users"></a>向用户显示对象数据

要向用户显示对象中的数据，请使用“数据源配置”向导创建对象数据源，然后从“数据源”窗口将整个对象或单个属性拖动到窗体 。

### <a name="modify-the-data-in-objects"></a>修改对象中的数据

若要编辑将数据绑定到 Windows 窗体控件的自定义对象中的数据，只需在绑定控件（或直接在对象属性中）中编辑数据即可。 数据绑定体系结构更新对象中的数据。

如果应用程序需要跟踪更改并回退其原始值建议的更改，则你必须在对象模型中实现此功能。 有关数据表如何跟踪建议的更改的示例，请参阅 <xref:System.Data.DataRowState>、<xref:System.Data.DataSet.HasChanges%2A> 和 <xref:System.Data.DataTable.GetChanges%2A>。

### <a name="save-data-in-objects-back-to-the-database"></a>将对象中的数据保存回数据库

通过将对象中的值传递给 TableAdapter 的 DBDirect 方法，来将数据保存回数据库。

Visual Studio 创建可直接对数据库执行的 DBDirect 方法。 这些方法不需要 DataSet 或 DataTable 对象。

|TableAdapter DBDirect 方法|说明|
| - |-----------------|
|`TableAdapter.Insert`|将新记录添加到数据库，使你可以将单个列值作为方法参数传递。|
|`TableAdapter.Update`|更新数据库中的现有记录。 Update 方法采用原始列值和新列值作为方法参数。 原始值用于查找原始记录，新值用于更新该记录。<br /><br /> `TableAdapter.Update` 方法还用于通过将 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> 或 <xref:System.Data.DataRow> 的数组作为方法参数，来协调返回数据库的数据集中的变化。|
|`TableAdapter.Delete`|基于作为方法参数传入的原始列值，从数据库中删除现有记录。|

若要从对象集合中保存数据，则请循环访问对象集合（例如使用下一个循环）。 使用 TableAdapter 的 DBDirect 方法将每个对象的值发送到数据库。

以下示例演示如何使用 `TableAdapter.Insert` DBDirect 方法将新的客户直接添加到数据库中：

:::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs" id="Snippet23":::
:::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb" id="Snippet23":::

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
