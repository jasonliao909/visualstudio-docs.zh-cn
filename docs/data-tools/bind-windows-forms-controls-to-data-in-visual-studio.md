---
title: 将 Windows 窗体控件绑定到数据
description: 将 Windows 窗体控件绑定到 Visual Studio 中的数据，以便向应用程序的用户显示数据。
ms.custom: SEO-VS-2020
ms.date: 11/03/2017
ms.topic: how-to
helpviewer_keywords:
- data [Windows Forms], data sources
- Windows Forms, data binding
- Windows Forms, displaying data
- displaying data on forms
- forms, displaying data
- data sources, displaying data
- displaying data, Windows Forms
- data [Windows Forms], displaying
ms.assetid: 243338ef-41af-4cc5-aff7-1e830236f0ec
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 311bdc7d0bf236f29d09804257aaaa8ce991f32f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601224"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 Windows 窗体控件绑定到数据

可通过将数据绑定到 Windows 窗体向应用程序的用户显示数据。 若要创建这些数据绑定的控件，请将项从“数据源”窗口拖动到 Visual Studio 中的 Windows 窗体设计器上。

![数据源拖动操作](../data-tools/media/raddata-data-source-drag-operation.png)

> [!TIP]
> 如果未显示“数据源”窗口，可通过选择“查看” > “其他窗口” > “数据源”，或者通过按 Shift+Alt+D 将其打开      。 必须在 Visual Studio 中打开一个项目才会显示“数据源”窗口。

在拖动项之前，你可设置要绑定到的控件类型。 所显示的值将不同，具体取决于是选择表本身还是单个列。  还可设置自定义值。 表的“详细信息”表示每个列都绑定到单独的控件。

![将数据源绑定到 DataGridView](../data-tools/media/raddata-bind-data-source-to-datagridview.png)

## <a name="bindingsource-and-bindingnavigator-controls"></a>BindingSource 和 BindingNavigator 控件

<xref:System.Windows.Forms.BindingSource> 组件有两个用途。 第一，在它将控件绑定到数据时提供抽象层。 窗体上的控件会绑定到 <xref:System.Windows.Forms.BindingSource> 组件，而不是直接绑定到数据源。 第二，它可以管理对象的集合。 向 <xref:System.Windows.Forms.BindingSource> 添加一个类型来创建该类型的列表。

有关 <xref:System.Windows.Forms.BindingSource> 组件的详细信息，请参阅：

- [BindingSource 组件](/dotnet/framework/winforms/controls/bindingsource-component)

- [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)

- [BindingSource 组件体系结构](/dotnet/framework/winforms/controls/bindingsource-component-architecture)

[BindingNavigator 控件](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)提供了一个用户界面，用于导航 Windows 应用程序显示的数据。

## <a name="bind-to-data-in-a-datagridview-control"></a>绑定到 DataGridView 控件中的数据

对于 [DataGridView 控件](/dotnet/framework/winforms/controls/datagridview-control-overview-windows-forms)，整个表将绑定到这一个控件。 将“DataGridView”拖动到窗体时，还会显示用于导航记录 (<xref:System.Windows.Forms.BindingNavigator>) 的工具条。 组件栏中将显示 [DataSet](../data-tools/dataset-tools-in-visual-studio.md)、[TableAdapter](../data-tools/create-and-configure-tableadapters.md)、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。 下图中还添加了一个 [TableAdapterManager](/previous-versions/bb384426(v=vs.140))，因为“Customers”表与“Orders”表相关。 这些变量在自动生成的代码中全部都声明为窗体类中的私有成员。 用于填充“DataGridView”的自动生成的代码位于 `Form_Load` 事件处理程序内。 用于保存数据以更新数据库的代码位于“BindingNavigator”的 `Save` 事件处理程序内。 你可根据需要移动或修改此代码。

![具有 BindingNavigator 的 GridView](../data-tools/media/raddata-gridview-with-bindingnavigator.png)

可通过单击每个的右上角的智能标记来自定义“DataGridView”和“BindingNavigator”的行为 ：

![DataGridView 和绑定导航器智能标记](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png)

如果“数据源”窗口中未提供应用程序所需的控件，可添加所需控件。 有关详细信息，请参阅[向“数据源”窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

还可将项从“数据源”窗口拖动到窗体上已有的控件上，从而将控件绑定到数据。 已绑定到数据的控件将其数据绑定重置为最近拖动到该控件上的项。 若要成为有效放置目标，控件必须能够显示从“数据源”窗口拖动到其上的项的基础数据类型。 例如，将数据类型为 <xref:System.DateTime> 的项拖动到 <xref:System.Windows.Forms.CheckBox> 上是无效的，因为 <xref:System.Windows.Forms.CheckBox> 不能显示日期。

## <a name="bind-to-data-in-individual-controls"></a>绑定到单独的控件中的数据

将数据源绑定到“详细信息”时，数据集中的每一列都将绑定到单独的控件。

![将数据源绑定到详细信息](../data-tools/media/raddata-bind-data-source-to-details.png)

> [!IMPORTANT]
> 请注意，上图是从“Customers”表的“Orders”属性拖动，而不是从“Orders”表拖动。 通过绑定到 `Customer.Orders` 属性，“DataGridView”中创建的导航命令会立即反映在详细信息控件中。 如果从“Orders”表拖动，控件仍将绑定到数据集，但不与“DataGridView”同步。

下图显示了默认数据绑定控件，这些控件是在“Customers”表中的“Orders”属性绑定到“数据源”窗口中的“详细信息”后添加到窗体的 。

![绑定到详细信息的“Orders”表](../data-tools/media/raddata-orders-table-bound-to-details.png)

另请注意，每个控件都有一个智能标记。 此标记启用仅适用于该控件的自定义。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Windows 窗体 (.NET Framework) 中的数据绑定](/dotnet/framework/winforms/windows-forms-data-binding)