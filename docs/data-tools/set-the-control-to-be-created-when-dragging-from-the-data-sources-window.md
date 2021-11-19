---
title: 设置拖动时要创建的控件
description: 了解如何设置在从“数据源”窗口拖动到 Visual Studio 中的 WPF 设计器或 Windows 窗体设计器时要创建的控件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Data Sources Window, select controls
- Windows Forms, displaying data
- data [Visual Studio], displaying on Windows Forms
- data [Visual Studio], Data Sources window
ms.assetid: 20597ff8-0c98-43ec-8fb1-05376804ba48
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 38d43074275db57180938e20fc242ff0a1524711
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601095"
---
# <a name="set-the-control-to-be-created-when-dragging-from-the-data-sources-window"></a>设置从“数据源”窗口中拖动时要创建的控件

可以通过将项从“数据源”窗口拖到 WPF 设计器或 Windows 窗体设计器上来创建数据绑定控件。 “数据源”窗口中的每个项都具有一个默认控件，当你将其拖动到设计器中时，将会创建该控件。 不过，可以选择创建不同的控件。

## <a name="set-the-controls-to-be-created-for-data-tables-or-objects"></a>设置要为数据表或对象创建的控件

在从“数据源”窗口拖动表示数据表或对象的项之前，可以选择在一个控件中显示所有数据，或在单独的控件中显示每个列或属性。

在此上下文中，术语“对象”是指自定义业务对象、实体（在实体数据模型中）或由服务返回的对象。

### <a name="to-set-the-controls-to-be-created-for-data-tables-or-objects"></a>设置要为数据表或对象创建的控件

1. 确保“WPF”设计器或“Windows 窗体”设计器处于打开状态 。

2. 在“数据源”窗口中，选择一个表示要设置的数据表或对象的项。

   > [!TIP]
   > 如果“数据源”窗口未打开，通过选择“查看” > “其他窗口” > “数据源”将其打开   。

3. 单击该项的下拉菜单，然后单击菜单中的以下项之一：

    - 若要在单独的控件中显示每个数据字段，请单击“详细信息”。 当你将数据项拖到设计器时，此操作将为父数据表或对象的每个列或属性创建不同的数据绑定控件，并为每个控件添加标签。

    - 若要在单个控件中显示所有数据，请在列表中选择一个不同的控件，例如 WPF 应用程序中的“DataGrid”或“列表”，或 Windows 窗体应用程序中的“DataGridView”  。

    可用控件列表取决于打开的设计器、项目所面向的 .NET 版本，以及是否添加了支持数据绑定到工具箱的自定义控件。 如果要创建的控件不在可用控件列表中，则可以将该控件添加到列表中。 有关详细信息，请参阅[向“数据源”窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

    若要了解如何创建可添加到“数据源”窗口中数据表或对象的控件列表中的自定义 Windows 窗体控件，请参阅[创建支持复杂数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)。

## <a name="set-the-controls-to-be-created-for-data-columns-or-properties"></a>设置要为数据列或属性创建的控件

可在将表示对象的列或属性的项从“数据源”窗口拖到设计器之前设置要创建的控件。

### <a name="to-set-the-controls-to-be-created-for-columns-or-properties"></a>设置要为列或属性创建的控件

1. 确保“WPF”设计器或“Windows 窗体”设计器处于打开状态 。

2. 在“数据源”窗口中，展开所需的表或对象以显示其列或属性。

3. 选择要为其设置要创建的控件的每个列或属性。

4. 单击列或属性的下拉菜单，然后在将项拖到设计器时选择要创建的控件。

     可用控件列表取决于打开的设计器、项目所面向的 .NET 版本，以及支持已添加到工具箱的数据绑定的自定义控件。 如果要创建的控件在可用控件列表中，则可以将该控件添加到列表中。 有关详细信息，请参阅[向“数据源”窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

     若要了解如何创建可添加到“数据源”窗口中数据列或属性的控件列表中的自定义控件，请参阅[创建支持简单数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)。

     如果不想为列或属性创建控件，请在下拉菜单中选择“无”。 如果要将父表或对象拖到设计器，但又不想包含特定的列或属性，这将非常有用。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
