---
title: 在 Windows 窗体应用程序中创建查找表
description: 了解如何在 Windows 窗体应用程序中创建查找表。 查找表描述绑定到两个相关数据表的控件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- lookup tables
- lookup tables, creating
ms.assetid: 0edd5385-c381-4b17-9096-74e2778db9d5
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 4d8bfc94d98c56d525d0d2d1c7f16f98cffbc7d0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601185"
---
# <a name="create-lookup-tables-in-windows-forms-applications"></a>在 Windows 窗体应用程序中创建查找表

查找表一词描述绑定到两个相关数据表的控件。 这些查找控件根据第二个表中所选的值显示第一个表中的数据。

可通过将父表的主节点（从[数据源](add-new-data-sources.md#data-sources-window)窗口）拖到窗体上已绑定到相关子表中的列的控件来创建查找表。

例如，请考虑销售数据库中的 `Orders` 表。 `Orders` 表中的每条记录都包括 `CustomerID`，用于指示下订单的客户。 `CustomerID` 是一个外键，它指向表 `Customers` 中的客户记录。 在这种情况下，在“数据源”窗口中展开 `Orders` 表，并将主节点设置为“详细信息” 。 然后将 `CustomerID` 列设置为使用 <xref:System.Windows.Forms.ComboBox>（或任何支持查找绑定的其他控件），并将 `Orders` 节点拖到窗体上。 最后将 `Customers` 节点拖动到绑定到相关列的控件上（在本例中，<xref:System.Windows.Forms.ComboBox> 绑定到 `CustomerID` 列）。

## <a name="to-databind-a-lookup-control"></a>对查找控件进行数据绑定

1. 打开项目后，通过选择“查看” > “其他窗口” > “数据源”，打开“数据源”窗口   。

    > [!NOTE]
    > 查找表要求在“数据源”窗口中提供两个相关表或对象。 有关详细信息，请参阅[数据集中的关系](relationships-in-datasets.md)。

2. 展开“数据源”窗口中的节点，直到可以看到父表及其所有列，以及相关的子表及其所有列。

    > [!NOTE]
    > 子表节点是在父表中显示为可展开子节点的节点。

3. 通过从子表的节点上的控件列表中选择“详细信息”，将子表的放置类型更改为“详细信息” 。 有关详细信息，请参阅[设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

4. 找到关联两个表的节点（上一示例中的 `CustomerID` 节点）。 通过从控件列表中选择 ComboBox，将其放置类型更改为 <xref:System.Windows.Forms.ComboBox>。

5. 将主子表节点从“数据源”窗口拖动到窗体上。

     该窗体上将显示数据绑定控件（带有说明性标签）和工具条 (<xref:System.Windows.Forms.BindingNavigator>)。 组件栏中将显示 [DataSet](../data-tools/dataset-tools-in-visual-studio.md)、[TableAdapter](../data-tools/create-and-configure-tableadapters.md)、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

6. 现在将主父表节点从“数据源”窗口直接拖动到查找控件上 (<xref:System.Windows.Forms.ComboBox>)。

     查找绑定现已建立。 对于在控件上设置的特定属性，请参阅下表。

    |属性|设置说明|
    |--------------| - |
    |**DataSource**|Visual Studio 将此属性设置拖到控件上的表所创建的 <xref:System.Windows.Forms.BindingSource>（相对于创建该控件时所创建的 <xref:System.Windows.Forms.BindingSource>）。<br /><br /> 如果需要进行调整，请将此属性设置为带有你要显示的列的表的 <xref:System.Windows.Forms.BindingSource>。|
    |**DisplayMember**|对于你拖动到控件上的表，则 Visual Studio 将此属性设置为该主键后的具有字符串数据类型的第一列。<br /><br /> 如果需要进行调整，请将此属性设置为要显示的列名称。|
    |**ValueMember**|Visual Studio 将此属性设置为参与主键的第一列，或表中的第一列（如果未定义任何键）。<br /><br /> 如果需要进行调整，请将此属性设置为带有你要显示的列的表的主键。|
    |**SelectedValue**|Visual Studio 将此属性设置为从“数据源”窗口中放置的原始列。<br /><br /> 如果需要进行调整，请将此属性设置为相关表中的外键列。|

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
