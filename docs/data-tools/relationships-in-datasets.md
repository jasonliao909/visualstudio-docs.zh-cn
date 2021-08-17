---
title: 创建数据集之间的关系
description: 在数据集之间创建Visual Studio。 了解 DataRelation 对象和约束。 在数据集管理器中手动创建数据关系。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122052689"
---
# <a name="create-relationships-between-datasets"></a>创建数据集之间的关系
包含相关数据表的数据集使用 对象来表示表 <xref:System.Data.DataRelation> 之间的父/子关系，并相互返回相关记录。 使用数据源配置向导 或 数据集设计器 **将相关** 表添加到数据集，可创建并 <xref:System.Data.DataRelation> 配置 对象。

对象 <xref:System.Data.DataRelation> 执行两个函数：

- 它可以提供与正在处理的记录相关的记录。 如果在父记录中 () 父记录，则它提供子记录;如果使用子记录 <xref:System.Data.DataRow.GetChildRows%2A> <xref:System.Data.DataRow.GetParentRow%2A> () 。

- 它可以强制执行引用完整性约束，例如删除父记录时删除相关的子记录。

了解真实联接和 对象函数的区别 <xref:System.Data.DataRelation> 非常重要。 在真正的联接中，记录取自父表和子表，并放入单个平面记录集。 使用 对象时 <xref:System.Data.DataRelation> ，不会创建任何新记录集。 相反，DataRelation 跟踪表之间的关系，并保持父记录和子记录同步。

## <a name="datarelation-objects-and-constraints"></a>DataRelation 对象和约束
<xref:System.Data.DataRelation>对象还用于创建和强制执行以下约束：

- 唯一约束，它保证表中的列不包含重复项。

- 外键约束，可用于维护数据集中父表和子表之间的引用完整性。

在 对象中指定的约束 <xref:System.Data.DataRelation> 通过自动创建适当的对象或设置属性实现。 如果使用 对象创建外键约束，则 类的实例 <xref:System.Data.DataRelation> <xref:System.Data.ForeignKeyConstraint> 将添加到对象的 <xref:System.Data.DataRelation> <xref:System.Data.DataRelation.ChildKeyConstraint%2A> 属性中。

通过简单地将数据列的 属性设置为 ，或者通过将 类的实例添加到 对象的 属性，实现唯 <xref:System.Data.DataColumn.Unique%2A> `true` <xref:System.Data.UniqueConstraint> <xref:System.Data.DataRelation> 一 <xref:System.Data.DataRelation.ParentKeyConstraint%2A> 约束。 有关在数据集中挂起约束的信息，请参阅在填充数据集 [时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。

### <a name="referential-integrity-rules"></a>引用完整性规则
作为外键约束的一部分，可以指定在三个点应用的引用完整性规则：

- 更新父记录时

- 删除父记录时

- 接受或拒绝更改时

你可以制定的规则在 枚举中 <xref:System.Data.Rule> 指定，下表列出了这些规则。

|外键约束规则|操作|
| - |------------|
|<xref:System.Data.Rule.Cascade>|对 (记录) 对父记录进行的任何更改也会在子表中的相关记录中进行。|
|<xref:System.Data.Rule.SetNull>|不会删除子记录，但子记录中的外键设置为 <xref:System.DBNull> 。 使用此设置时，子记录可以保留为"孤立"，也就是说，它们与父记录没有关系。 **注意：** 使用此规则可能会导致子表中的数据无效。|
|<xref:System.Data.Rule.SetDefault>|相关子记录中的外键设置为其默认值， (列的 属性集建立 <xref:System.Data.DataColumn.DefaultValue%2A>) 。|
|<xref:System.Data.Rule.None>|不更改相关子记录。 使用此设置时，子记录可以包含对无效父记录的引用。|

有关数据集表中的更新详细信息，请参阅 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)。

### <a name="constraint-only-relations"></a>仅约束关系
创建 对象时，可以选择指定关系仅用于强制实施约束，也就是说，它也不用于 <xref:System.Data.DataRelation> 访问相关记录。 可以使用此选项生成一个比具有相关记录功能的方法略高效且包含更少方法的数据集。 但是，你将无法访问相关记录。 例如，仅约束关系会阻止删除仍具有子记录的父记录，并且无法通过父记录访问子记录。

## <a name="manually-creating-a-data-relation-in-the-dataset-designer"></a>手动创建数据关系数据集设计器
使用数据表中的数据设计工具创建数据Visual Studio，如果可以从数据源中收集信息，则会自动创建关系。 如果从"工具箱"的"**数据集**"选项卡手动添加数据表，可能需要手动创建关系。 有关以编程 <xref:System.Data.DataRelation> 方式创建对象的信息，请参阅 [添加 DataRelations](/dotnet/framework/data/adonet/dataset-datatable-dataview/adding-datarelations)。

数据表之间的关系显示为 数据集设计器 **中的行**，其中键和无穷大字形描述了关系的一对多方面。 默认情况下，关系的名称不会出现在设计图面上。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-create-a-relationship-between-two-data-tables"></a>在两个数据表之间创建关系

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅演练： [在](walkthrough-creating-a-dataset-with-the-dataset-designer.md)数据集设计器。

2. 将 **"关系"** 对象从 **"数据集"工具箱** 拖到关系中的子数据表上。

     "**关系**"对话框随即打开，用将"关系"对象拖动到的表填充"子 **表"** 框。

3. 从"父表" **框中选择父** 表。 父表包含一对多关系的"一"端上的记录。

4. 验证"子表"框中是否显示了 **正确的子** 表。 子表包含一对多关系的"多"端上的记录。

5. 在"名称"框中键入 **关系的名称，** 或保留基于所选表的默认名称。 这是代码中实际 <xref:System.Data.DataRelation> 对象的名称。

6. 选择联接"键列"和"外键列" **列表中** 表 **的** 列。

7. 选择是创建关系、约束还是同时创建关系和/或约束。

8. 选择或清除 **"嵌套关系"** 框。 选择此选项将 属性设置为 ，当这些行作为 XML 数据写入或与 同步时，它会导致关系子行嵌套在父 <xref:System.Data.DataRelation.Nested%2A> `true` 列中 <xref:System.Xml.XmlDataDocument> 。 有关详细信息，请参阅嵌套 [DataRelations](/dotnet/framework/data/adonet/dataset-datatable-dataview/nesting-datarelations)。

9. 设置更改这些表中的记录时要强制实施的规则。 有关详细信息，请参阅 <xref:System.Data.Rule>。

10. 单击 **"** 确定"创建关系。 两个表之间的设计器上将显示关系线。

#### <a name="to-display-a-relation-name-in-the-dataset-designer"></a>在消息中显示关系数据集设计器

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅演练： [在](walkthrough-creating-a-dataset-with-the-dataset-designer.md)数据集设计器。

2. 在" **数据"** 菜单中，选择" **显示关系标签"** 命令以显示关系名称。 清除该命令以隐藏关系名称。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)
