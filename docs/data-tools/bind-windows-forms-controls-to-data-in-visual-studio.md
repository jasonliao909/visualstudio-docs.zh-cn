---
title: 将 Windows 窗体控件绑定到数据
description: 将Windows窗体控件绑定到 Visual Studio，以便向应用程序的用户显示数据。
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
ms.openlocfilehash: d891cc83008c844ddc694b958be6314c9f2de63a7c8383a541fc3ccd265d00bc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121240635"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 Windows 窗体控件绑定到数据

可以通过将数据绑定到窗体，向应用程序的用户Windows数据。 若要创建这些数据绑定控件，请将项从"数据源"窗口拖动到Windows窗体设计器Visual Studio。

![数据源拖动操作](../data-tools/media/raddata-data-source-drag-operation.png)

> [!TIP]
> 如果"**数据源"** 窗口不可见，则可以通过选择"查看其他数据源Windows或按 Shift Alt D  >  **来**  >   + **打开** + **它**。 必须打开一个项目，Visual Studio"**数据源"** 窗口。

在拖动项之前，可以设置要绑定到的控件的类型。 将显示不同的值，具体取决于是选择表本身还是单个列。  还可以设置自定义值。 对于表 **，"详细信息** "表示每个列都绑定到单独的控件。

![将数据源绑定到 DataGridView](../data-tools/media/raddata-bind-data-source-to-datagridview.png)

## <a name="bindingsource-and-bindingnavigator-controls"></a>BindingSource 和 BindingNavigator 控件

<xref:System.Windows.Forms.BindingSource> 组件有两个用途。 首先，它将控件绑定到数据时提供抽象层。 窗体上的控件绑定到组件 <xref:System.Windows.Forms.BindingSource> ，而不是直接绑定到数据源。 其次，它可以管理 对象的集合。 将类型添加到 <xref:System.Windows.Forms.BindingSource> 会创建该类型的列表。

有关 组件的信息 <xref:System.Windows.Forms.BindingSource> ，请参阅：

- [BindingSource 组件](/dotnet/framework/winforms/controls/bindingsource-component)

- [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)

- [BindingSource 组件体系结构](/dotnet/framework/winforms/controls/bindingsource-component-architecture)

[BindingNavigator](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)控件提供了一个用户界面，用于导航应用程序Windows数据。

## <a name="bind-to-data-in-a-datagridview-control"></a>绑定到 DataGridView 控件中的数据

对于 [DataGridView 控件](/dotnet/framework/winforms/controls/datagridview-control-overview-windows-forms)，整个表绑定到该单个控件。 将 **DataGridView** 拖动到窗体时，还会显示用于导航记录 () <xref:System.Windows.Forms.BindingNavigator> 条。 数据集[](../data-tools/dataset-tools-in-visual-studio.md)[、TableAdapter](../data-tools/create-and-configure-tableadapters.md)、 <xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator> 将显示在组件栏中。 下图还添加了 [TableAdapterManager，](/previous-versions/bb384426(v=vs.140)) 因为 Customers 表与 Orders 表相关。 这些变量全部在自动生成的代码中声明为窗体类中的私有成员。 用于填充 **DataGridView** 的自动生成的代码位于 事件 `Form_Load` 处理程序中。 用于保存数据以更新数据库的代码位于 `Save` **BindingNavigator 的事件处理程序中**。 可以根据需要移动或修改此代码。

![具有 BindingNavigator 的 GridView](../data-tools/media/raddata-gridview-with-bindingnavigator.png)

可以通过单击每个项右上角的智能标记来自定义 **DataGridView** 和 **BindingNavigator** 的行为：

![DataGridView 和绑定导航器智能标记](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png)

如果应用程序所需的控件在"数据源"窗口中 **不可用，可以** 添加控件。 有关详细信息，请参阅 [向"数据源"窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

还可以将项从"数据源 **"** 窗口拖动到窗体上已有的控件上，以将控件绑定到数据。 已绑定到数据的控件将数据绑定重置为最近拖动到它的项。 若要成为有效的放置目标，控件必须能够显示从"数据源"窗口拖动到该项 **上的基础** 数据类型。 例如，将数据类型为 的项拖到 上是无效的，因为 无法 <xref:System.DateTime> <xref:System.Windows.Forms.CheckBox> <xref:System.Windows.Forms.CheckBox> 显示日期。

## <a name="bind-to-data-in-individual-controls"></a>绑定到单个控件中的数据

将数据源绑定到 **Details** 时，数据集的每一列都绑定到单独的 控件。

![将数据源绑定到详细信息](../data-tools/media/raddata-bind-data-source-to-details.png)

> [!IMPORTANT]
> 请注意，在上图中，从 Customers 表的 Orders 属性拖动，而不是从 Orders 表拖动。 通过绑定到 `Customer.Orders` 属性 **，DataGridView** 中的导航命令会立即反映在详细信息控件中。 如果从 Orders 表拖动，控件仍将绑定到数据集，但不与 **DataGridView 同步**。

下图显示了在 Customers 表中的 Orders 属性绑定到"数据源"窗口中的"详细信息"后添加到窗体 **的默认数据绑定** 控件。

![绑定到详细信息的订单表](../data-tools/media/raddata-orders-table-bound-to-details.png)

另请注意，每个控件都有一个智能标记。 此标记启用仅适用于该控件的自定义项。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Windows 窗体 (.NET Framework) ](/dotnet/framework/winforms/windows-forms-data-binding)