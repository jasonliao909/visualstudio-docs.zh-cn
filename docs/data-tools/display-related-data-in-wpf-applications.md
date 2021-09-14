---
title: 在 WPF 应用程序中显示相关数据
description: 在 WPF 应用程序中显示相关的数据。 在父子关系中处理多个表或实体中彼此相关的数据。
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
ms.assetid: 3aa80194-0191-474d-9d28-5ec05654b426
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: c5cf789d120249ca283d655f59f5058a7b28f207
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601168"
---
# <a name="display-related-data-in-wpf-applications"></a>在 WPF 应用程序中显示相关数据

在某些应用程序中，你可能想要处理来自多个表或实体的数据，这些表或实体在父子关系中彼此相关。 例如，你可能想要显示一个网格，用于显示表中的 `Customers` 客户。 当用户选择特定客户时，另一个网格显示相关表中的该客户 `Orders` 的订单。

可以通过将项从"数据源"窗口拖动到 WPF 设计器来创建显示相关数据的数据绑定控件。

## <a name="to-create-controls-that-display-related-records"></a>创建显示相关记录的控件

1. 在“数据”菜单上单击“显示数据源”，打开“数据源”窗口。

2. 单击“添加新数据源”，然后完成“数据源配置”向导。

3. 打开 WPF 设计器，并确保设计器包含一个容器，该容器是"数据源"窗口中项 **的有效放置** 目标。

     有关有效放置目标详细信息，请参阅将[WPF 控件绑定到](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)Visual Studio。

4. 在 **"数据源"** 窗口中，展开表示关系中的父表或对象的节点。 父表或对象位于一对多关系的"一"端。

5. 将父节点 (父节点或父节点中) 项从"数据源"窗口拖动到设计器中的有效放置目标上。

     Visual Studio生成 XAML，为拖动的每个项创建新的数据绑定控件。 XAML 还会将父表或对象的新 添加到 <xref:System.Windows.Data.CollectionViewSource> 放置目标的资源。 对于某些数据源，Visual Studio生成代码以将数据加载到父表或对象中。 有关详细信息，请参阅将[WPF 控件绑定到](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)Visual Studio。

6. 在" **数据源"** 窗口中，找到相关的子表或对象。 相关子表和对象在父节点的数据列表底部显示为可展开节点。

7. 将子节点 (子节点或子节点中) 项从"数据源"窗口拖动到设计器中的有效放置目标上。

     Visual Studio生成 XAML，为拖动的每个项创建新的数据绑定控件。 XAML 还会将子 <xref:System.Windows.Data.CollectionViewSource> 表或对象的新 添加到放置目标的资源。 此新 绑定到刚拖动到设计器的父表 <xref:System.Windows.Data.CollectionViewSource> 或对象的 属性。 对于某些数据源，Visual Studio生成代码以将数据加载到子表或对象中。

     下图演示了"数据源 **"** 窗口中数据集 **中 Customers** 表 **的相关 Orders** 表。

     ![显示关系的数据源窗口](../data-tools/media/datasources2.gif)

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [在 WPF 应用程序中创建查找表](../data-tools/create-lookup-tables-in-wpf-applications.md)
