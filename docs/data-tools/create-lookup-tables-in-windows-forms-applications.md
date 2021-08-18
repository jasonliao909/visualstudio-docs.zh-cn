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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122052923"
---
# <a name="create-lookup-tables-in-windows-forms-applications"></a>在 Windows 窗体应用程序中创建查找表

术语 *查找表* 描述绑定到两个相关数据表的控件。 这些查找控件基于第二个表中所选的值显示第一个表中的数据。

可以通过将父表的主节点 (从"数据源" [窗口) 拖动](add-new-data-sources.md#data-sources-window) 到已绑定到相关子表中的列的窗体上的控件上来创建查找表。

例如，请考虑销售 `Orders` 数据库中的 表。 表中的每条 `Orders` 记录都包括 `CustomerID` ，指示哪个客户下订单。 `CustomerID`是指向表中的客户记录的外 `Customers` 键。 在此方案中，展开"数据源" `Orders` 窗口中 **的** 表，将主节点设置为"详细信息 **"。** 然后，将列设置为使用 (支持查找绑定的其他任何控件，) `CustomerID` <xref:System.Windows.Forms.ComboBox> `Orders` 节点拖动到窗体上。 最后，将节点拖动到绑定到相关列的控件上，在这种情况下，将 `Customers` <xref:System.Windows.Forms.ComboBox> 绑定到 `CustomerID` 该列。

## <a name="to-databind-a-lookup-control"></a>对查找控件进行数据绑定

1. 打开项目后，通过选择"**查看其他数据源**"打开  >  **"Windows**  >  **数据源"。**

    > [!NOTE]
    > 查找表要求在"数据源"窗口中提供两个 **相关的表或** 对象。 有关详细信息，请参阅数据集 [中的关系](relationships-in-datasets.md)。

2. 展开"数据源"窗口中的节点，直到可以看到父表及其所有列，以及相关的子表及其所有列。

    > [!NOTE]
    > 子表节点是作为父表中的可展开子节点出现的节点。

3. 通过从子表节点上的控件列表中选择"详细信息"，将子表的删除类型更改为"详细信息"。 有关详细信息，请参阅设置从"数据源"窗口拖动时 [要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

4. 找到与上一示例中的节点 (`CustomerID` 表相关的节点) 。 从控件列表中选择 <xref:System.Windows.Forms.ComboBox> **ComboBox，将放置** 类型更改为 。

5. 将主子表节点从" **数据源"窗口** 拖到窗体上。

     数据绑定 (具有描述性) 标签和工具条 () <xref:System.Windows.Forms.BindingNavigator> 显示在窗体上。 数据集[](../data-tools/dataset-tools-in-visual-studio.md)[、TableAdapter](../data-tools/create-and-configure-tableadapters.md)、 <xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator> 将显示在组件栏中。

6. 现在，将主父表节点从"数据源"窗口直接拖动到 <xref:System.Windows.Forms.ComboBox> () 。

     现已建立查找绑定。 有关在 控件上设置的特定属性，请参阅下表。

    |属性|设置说明|
    |--------------| - |
    |**DataSource**|Visual Studio 将此属性设置拖到控件上的表所创建的 <xref:System.Windows.Forms.BindingSource>（相对于创建该控件时所创建的 <xref:System.Windows.Forms.BindingSource>）。<br /><br /> 如果需要进行调整，请用要显示的列将此选项设置为 <xref:System.Windows.Forms.BindingSource> 表的 。|
    |**DisplayMember**|对于你拖动到控件上的表，则 Visual Studio 将此属性设置为该主键后的具有字符串数据类型的第一列。<br /><br /> 如果需要进行调整，请设置为要显示的列名。|
    |**ValueMember**|Visual Studio 将此属性设置为参与主键的第一列，或表中的第一列（如果未定义任何键）。<br /><br /> 如果需要进行调整，请用要显示的列将此选项设置为表中的主键。|
    |**SelectedValue**|Visual Studio将此属性设置到从"数据源"窗口 **删除的原始** 列。<br /><br /> 如果需要进行调整，请设置为相关表中的外键列。|

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
