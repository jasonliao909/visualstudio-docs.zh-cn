---
title: 创建数据集之间的关系
description: 在 Visual Studio 中创建数据集之间的关系。 了解 DataRelation 对象和约束。 在数据集管理器中手动创建数据关系。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vbData.Microsoft.VSDesigner.DataSource.DesignRelation
- vbdata.Microsoft.VSDesigner.DataSource.DesignRelation
helpviewer_keywords:
- relationships, about relationships
- datasets [Visual Basic], relationships
- relationships, datasets
ms.assetid: cfe274f0-71fe-40f6-994e-7c7f6273c9ba
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 40a964f6b5d21f2e5a601cd81d33fafbdd030189
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601113"
---
# <a name="create-relationships-between-datasets"></a>创建数据集之间的关系
包含相关数据表的数据集使用 <xref:System.Data.DataRelation> 对象来表示表之间的父/子关系，并返回彼此相关的记录。 通过使用 " **数据源配置向导**" 或 **数据集设计器** 向数据集添加相关表， <xref:System.Data.DataRelation> 可为您创建和配置对象。

<xref:System.Data.DataRelation>对象执行两个函数：

- 它可以使与您正在使用的记录相关的记录可用。 如果你位于父记录中，则它提供子记录 (<xref:System.Data.DataRow.GetChildRows%2A>) 和父记录（如果你使用的是子记录 (<xref:System.Data.DataRow.GetParentRow%2A>) 。

- 它可以强制实施引用完整性约束，例如删除父记录时删除相关子记录。

了解真正的联接与对象的函数之间的差异非常重要 <xref:System.Data.DataRelation> 。 在真正的联接中，记录取自父表和子表，并放入单个平面记录集中。 使用 <xref:System.Data.DataRelation> 对象时，不会创建新的记录集。 而 DataRelation 会跟踪表之间的关系，并使父记录和子记录保持同步。

## <a name="datarelation-objects-and-constraints"></a>DataRelation 对象和约束
<xref:System.Data.DataRelation>对象还用于创建和强制执行以下约束：

- Unique 约束，保证表中的列不包含重复项。

- 外键约束，可用于维护数据集中的父表和子表之间的引用完整性。

在对象中指定的约束 <xref:System.Data.DataRelation> 是通过自动创建适当的对象或设置属性来实现的。 如果使用对象创建外键约束，则类的 <xref:System.Data.DataRelation> 实例 <xref:System.Data.ForeignKeyConstraint> 将添加到 <xref:System.Data.DataRelation> 对象的 <xref:System.Data.DataRelation.ChildKeyConstraint%2A> 属性。

只需将 <xref:System.Data.DataColumn.Unique%2A> 数据列的属性设置为 `true` 或将类的实例添加 <xref:System.Data.UniqueConstraint> 到 <xref:System.Data.DataRelation> 对象的 <xref:System.Data.DataRelation.ParentKeyConstraint%2A> 属性即可实现唯一约束。 有关挂起数据集中的约束的信息，请参阅在 [填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

### <a name="referential-integrity-rules"></a>引用完整性规则
作为外键约束的一部分，你可以指定应用于三个点的引用完整性规则：

- 更新父记录时

- 删除父记录时

- 接受或拒绝更改时

可以进行的规则在枚举中指定 <xref:System.Data.Rule> ，并在下表中列出。

|外键约束规则|操作|
| - |------------|
|<xref:System.Data.Rule.Cascade>|对父记录所做的更改 (更新或删除) 也在子表中的相关记录中进行。|
|<xref:System.Data.Rule.SetNull>|子记录不会被删除，但子记录中的外键会设置为 <xref:System.DBNull> 。 使用此设置时，子记录可以保留为 "孤立项"，也就是说，它们与父记录之间没有关系。 **注意：** 使用此规则可能导致子表中的数据无效。|
|<xref:System.Data.Rule.SetDefault>|相关子记录中的外键设置为其默认值 (如) 的属性所确定 <xref:System.Data.DataColumn.DefaultValue%2A> 。|
|<xref:System.Data.Rule.None>|对相关子记录不进行任何更改。 对于此设置，子记录可能包含对无效父记录的引用。|

有关数据集表中的更新的详细信息，请参阅 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)。

### <a name="constraint-only-relations"></a>仅限约束关系
当您创建 <xref:System.Data.DataRelation> 对象时，您可以选择指定该关系仅用于强制约束，也就是说，它也不会用于访问相关记录。 您可以使用此选项生成一个数据集，该数据集的效率略高，且包含的方法比相关记录功能少。 但是，您将无法访问相关记录。 例如，仅限约束关系可防止删除仍具有子记录的父记录，并且不能通过父记录访问子记录。

## <a name="manually-creating-a-data-relation-in-the-dataset-designer"></a>在数据集设计器中手动创建数据关系
使用 Visual Studio 中的数据设计工具创建数据表时，如果可以从数据源收集信息，将自动创建关系。 如果从 "**工具箱**" 的 "**数据集**" 选项卡手动添加数据表，则可能必须手动创建关系。 有关 <xref:System.Data.DataRelation> 以编程方式创建对象的信息，请参阅 [添加 datarelation](/dotnet/framework/data/adonet/dataset-datatable-dataview/adding-datarelations)。

数据表之间的关系在 **数据集设计器** 中显示为线条，并具有键和无穷标志符号，用于描述关系的一对多方面。 默认情况下，关系的名称不会显示在设计图面上。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-create-a-relationship-between-two-data-tables"></a>创建两个数据表之间的关系

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅 [演练：在数据集设计器中创建数据集](walkthrough-creating-a-dataset-with-the-dataset-designer.md)。

2. 将 **关系** 对象从 **数据集** 工具箱拖动到关系中的子数据表。

     " **关系** " 对话框将打开，并将 **子表** 框填充到您将 **关系** 对象拖到其中的表。

3. 从 " **父表** " 框中选择父表。 父表包含一对多关系的 "一" 端上的记录。

4. 验证 **子** 表框中是否显示了正确的子表。 子表包含一对多关系的 "多" 方上的记录。

5. 在 " **名称** " 框中键入关系的名称，或保留基于所选表的默认名称。 这是 <xref:System.Data.DataRelation> 代码中实际对象的名称。

6. 在 " **键列** " 和 " **外键列** " 列表中选择联接表的列。

7. 选择是要创建关系还是约束，或同时创建两者。

8. 选中或清除 " **嵌套关系** " 框。 如果选择此选项，则将 <xref:System.Data.DataRelation.Nested%2A> 属性设置为 `true` ，并在将这些行写入为 XML 数据或与同步时，使关系的子行嵌套在父列中 <xref:System.Xml.XmlDataDocument> 。 有关详细信息，请参阅 [嵌套 datarelation](/dotnet/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations)。

9. 设置对这些表中的记录进行更改时要强制执行的规则。 有关详细信息，请参阅 <xref:System.Data.Rule>。

10. 单击 **"确定"** 以创建关系。 关系线出现在设计器中的两个表之间。

#### <a name="to-display-a-relation-name-in-the-dataset-designer"></a>在数据集设计器中显示关系名称

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅 [演练：在数据集设计器中创建数据集](walkthrough-creating-a-dataset-with-the-dataset-designer.md)。

2. 从 " **数据** " 菜单中，选择 " **显示关系标签** " 命令以显示关系名称。 清除该命令以隐藏关系名称。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)
