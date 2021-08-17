---
title: 在 WPF 应用程序中创建查找表
description: 在 WPF 应用中创建查找表。 查找表是一种控件，它基于另一个表中的外键字段值显示数据表中的信息。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122052936"
---
# <a name="create-lookup-tables-in-wpf-applications"></a>在 WPF 应用程序中创建查找表

术语 *查找* 表 (有时称为查找 *绑定) 描述* 一个控件，该控件基于另一个表中的外键字段的值显示一个数据表中的信息。 可以通过将"数据源"窗口中父表或对象的主节点拖到已绑定到相关子表中的列或属性的控件上来创建查找表。

例如，请考虑销售 `Orders` 数据库中的 表。 表中的每条 `Orders` 记录都包括一 `CustomerID` 个 ，用于指示哪个客户下订单。 `CustomerID`是指向表中的客户记录的外 `Customers` 键。 显示表中的订单列表时， `Orders` 可能需要显示实际客户名称，而不是 `CustomerID` 。 由于客户名称位于 `Customers` 表中，因此你需要创建一个查找表以显示客户名称。 查找表使用 `CustomerID` 记录中的 `Orders` 值来导航关系，并返回客户名称。

## <a name="to-create-a-lookup-table"></a>创建查找表的步骤

1. 将具有相关数据的以下数据源类型之一添加到项目：

    - 数据集或实体数据模型。

    - WCF 数据服务、WCF 服务或 Web 服务。 有关详细信息，请参阅[如何：连接服务中的数据。](../data-tools/how-to-connect-to-data-in-a-service.md)

    - 对象。 有关详细信息，请参阅绑定到 中[Visual Studio。](bind-objects-in-visual-studio.md)

    > [!NOTE]
    > 必须先将两个相关表或对象作为项目的数据源存在，然后才能创建查找表。

2. 打开 **WPF 设计器**，并确保设计器包含一个容器，该容器是"数据源"窗口中项 **的有效放置** 目标。

     有关有效放置目标的信息，请参阅将[WPF 控件绑定到](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)Visual Studio。

3. 在“数据”菜单上单击“显示数据源”，打开“数据源”窗口。

4. 展开"数据源"窗口中 **的** 节点，直到可以看到父表或对象以及相关的子表或对象。

    > [!NOTE]
    > 相关子表或对象是作为可展开子节点显示在父表或对象下的节点。

5. 单击子节点的下拉菜单，然后选择"详细信息 **"。**

6. 展开子节点。

7. 在子节点下，单击与子数据和父数据相关的项的下拉菜单。  (前面的示例中，这是 **CustomerID** node.) 选择以下支持查找绑定的控件类型之一：

    - **ComboBox**

    - **ListBox**

    - **ListView**

        > [!NOTE]
        > 如果 **ListBox** 或 **ListView** 控件未显示在列表中，可以将这些控件添加到列表中。 有关信息， [请参阅设置从"数据源"窗口拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

    - 派生自 的任何自定义控件 <xref:System.Windows.Controls.Primitives.Selector> 。

        > [!NOTE]
        > 若要了解如何将自定义控件添加到可以在"数据源"窗口中为项选择的控件列表中，请参阅向"数据源"[窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

8. 将子节点从"数据源 **"窗口** 拖到 WPF 设计器中的容器上。  (前面的示例中，子节点是 **Orders** node.) 

     Visual Studio生成 XAML，为拖动的每个项创建新的数据绑定控件。 XAML 还会将子 <xref:System.Windows.Data.CollectionViewSource> 表或对象的新 添加到放置目标的资源。 对于某些数据源，Visual Studio生成代码以将数据加载到表或对象中。 有关详细信息，请参阅将[WPF 控件绑定到](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)Visual Studio。

9. 将父节点从"数据源 **"** 窗口拖到前面创建的查找绑定控件上。  (前面的示例中，父节点是"客户 **"节点**) 。

     Visual Studio控件上设置一些属性以配置查找绑定。 下表列出了要修改Visual Studio属性。 如有必要，可以在 XAML 或"属性" **窗口中更改这些属性** 。

    |属性|设置说明|
    |--------------| - |
    |<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>|此属性指定用于获取控件中显示的数据的集合或绑定。 Visual Studio将此属性设置 <xref:System.Windows.Data.CollectionViewSource> 为拖动到控件的父数据的 。|
    |<xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A>|此属性指定控件中显示的数据项的路径。 Visual Studio将此属性设置到父数据中具有字符串数据类型的主键之后的第一列或属性。<br /><br /> 如果要在父数据中显示其他列或属性，请将此属性更改为其他属性的路径。|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A>|Visual Studio将此属性绑定到拖动到设计器的子数据的列或属性。 这是父数据的外键。|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValuePath%2A>|Visual Studio将此属性设置到作为父数据的外键的子数据的列或属性的路径。|

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)
- [演练：在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)
