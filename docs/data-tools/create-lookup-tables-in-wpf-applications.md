---
title: 在 WPF 应用程序中创建查找表
description: 在 WPF 应用中创建查找表。 查找表是一个控件，它显示数据表中基于另一个表中的外键字段值的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 56a1fbff-c7e8-4187-a1c1-ffd17024bc1b
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 52c14b4fd8369db5df57579ea20b3ff9e17c898f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601184"
---
# <a name="create-lookup-tables-in-wpf-applications"></a>在 WPF 应用程序中创建查找表

术语“查找表”（有时称作“查找绑定”）是一个控件，该控件显示数据表中基于另一个表中的外键字段值的信息 。 可通过将“数据源”窗口中父表或对象的主节点拖到已绑定到相关子表中的列或属性的控件来创建查找表。

例如，请考虑销售数据库中的 `Orders` 表。 `Orders` 表中的每条记录都包括指示下订单的客户的 `CustomerID`。 `CustomerID` 是一个外键，它指向表 `Customers` 中的客户记录。 显示 `Orders` 表中的订单列表时，可能需要显示实际的客户姓名，而不是 `CustomerID`。 由于客户姓名位于 `Customers` 表中，因此需要创建查找表以显示客户姓名。 查找表使用 `Orders` 记录中的 `CustomerID` 值来导航关系，并返回客户姓名。

## <a name="to-create-a-lookup-table"></a>创建查找表的步骤

1. 将以下类型的数据源之一添加到你的项目中：

    - 数据集或实体数据模型。

    - WCF 数据服务、WCF 服务或 Web 服务。 有关详细信息，请参阅 [如何：连接到服务中的数据](../data-tools/how-to-connect-to-data-in-a-service.md)。

    - 对象。 有关详细信息，请参阅在[绑定到 Visual Studio 中的对象](bind-objects-in-visual-studio.md)。

    > [!NOTE]
    > 创建查找表之前，必须有两个相关的表或对象作为项目的数据源。

2. 打开“WPF 设计器”，并确保设计器包含一个容器，该容器是“数据源”窗口中项的有效放置目标 。

     有关有效放置目标的详细信息，请参阅[将 WPF 控件绑定到 Visual Studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)。

3. 在“数据”菜单上单击“显示数据源”，打开“数据源”窗口。

4. 展开“数据源”窗口中的节点，直到可以看到父表或对象以及相关的子表或对象。

    > [!NOTE]
    > 相关的子表或对象是显示为父表或对象下的可扩展子节点的节点。

5. 单击子节点的下拉菜单，并选择“详细信息”。

6. 展开子节点。

7. 在子节点下，单击与子数据和父数据相关联的项的下拉菜单。 （在前面的示例中，这是 CustomerID 节点。）选择支持查找绑定的以下控件类型之一：

    - **ComboBox**

    - **ListBox**

    - **ListView**

        > [!NOTE]
        > 如果列表中未显示 ListBox 或 ListView 控件，则可以将这些控件添加到列表 。 有关详细信息，请参阅[设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

    - 派生自 <xref:System.Windows.Controls.Primitives.Selector> 的任何自定义控件。

        > [!NOTE]
        > 有关如何将自定义控件添加到控件列表（可从中选择适用于“数据源”窗口中的项的控件）的信息，请参阅[将自定义控件添加到“数据源”窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

8. 将子节点从“数据源”窗口拖到 WPF 设计器中的容器上。 （在上文的示例中，子节点是 Orders 节点）

     Visual Studio 生成 XAML，它会创建适用于拖动的每个项的新数据绑定控件。 XAML 还会将适用于子表或对象的新 <xref:System.Windows.Data.CollectionViewSource> 添加到拖放目标的资源。 对于某些数据源，Visual Studio 还会生成代码，以便将数据加载到表或对象。 有关详细信息，请参阅[将 WPF 控件绑定到 Visual Studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)。

9. 将父节点从“数据源”窗口拖到前面创建的查找绑定控件上。 （在上文的示例中，父节点是 Customers 节点）。

     Visual Studio 设置控件上的某些属性以配置查找绑定。 下表列出了 Visual Studio 修改的属性。 如果需要，可以在 XAML 或“属性”窗口中更改这些属性。

    |属性|设置说明|
    |--------------| - |
    |<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>|此属性指定用于获取控件中显示的数据的集合或绑定。 Visual Studio 将此属性设置为拖动到控件的父数据的 <xref:System.Windows.Data.CollectionViewSource>。|
    |<xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A>|此属性指定控件中显示的数据项的路径。 Visual Studio 将此属性设置为父数据中具有字符串数据类型的第一列或属性（在主键之后）。<br /><br /> 如果要在父数据中显示其他列或属性，请将此属性更改为其他属性的路径。|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A>|Visual Studio 将此属性绑定到拖到设计器中的子数据的列或属性。 这是父数据的外键。|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValuePath%2A>|Visual Studio 将此属性设置为子数据（父数据的外键）的列或属性的路径。|

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)
- [演练：在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)
