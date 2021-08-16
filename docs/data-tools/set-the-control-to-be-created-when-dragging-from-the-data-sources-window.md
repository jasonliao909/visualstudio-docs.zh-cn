---
title: 设置拖动时要创建的控件
description: 了解如何在将控件从"数据源"窗口拖动到 WPF 设计器或 Windows 窗体设计器时设置要创建的Visual Studio。
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
ms.openlocfilehash: 1033ffad781efe15507c5a484cd83f88a837d00fb6bc28fc5df78404076d6361
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121346825"
---
# <a name="set-the-control-to-be-created-when-dragging-from-the-data-sources-window"></a>设置从“数据源”窗口中拖动时要创建的控件

可以通过将项从"数据源"窗口拖动到 WPF设计器或窗体设计器Windows控件。 "数据源 **"窗口中的每个** 项都有一个默认控件，该控件在拖动到设计器时创建。 但是，可以选择创建其他控件。

## <a name="set-the-controls-to-be-created-for-data-tables-or-objects"></a>设置要为数据表或对象创建的控件

在从"数据源"窗口中拖动表示数据表或对象的项之前，可以选择在一个控件中显示所有数据，或在单独的控件中显示每个列或属性。

在此上下文中，术语 *"对象* "是指自定义业务对象、 (实体对象实体数据模型) 服务返回的对象。

### <a name="to-set-the-controls-to-be-created-for-data-tables-or-objects"></a>设置要为数据表或对象创建的控件

1. 请确保 **WPF 设计器** 或 Windows **窗体** 设计器已打开。

2. 在 **"数据源"** 窗口中，选择表示要设置的数据表或对象的项。

   > [!TIP]
   > 如果 **"数据源"** 窗口未打开，可以通过选择"查看数据源的其他Windows  >    >  **打开它**。

3. 单击该项的下拉菜单，然后在菜单中单击以下项之一：

    - 若要在单独的控件中显示每个数据字段，请单击"详细信息 **"。** 将数据项拖动到设计器时，此操作将为父数据表或对象的每个列或属性以及每个控件的标签创建不同的数据绑定控件。

    - 若要在单个控件中显示所有数据，请在列表中选择其他控件，例如 WPF 应用程序中的 **DataGrid** 或 **List，** 或 Windows 窗体应用程序中的 **DataGridView。**

    可用控件的列表取决于已打开的设计器、项目面向的 .NET 版本，以及是否添加了支持数据绑定到工具箱 的 **自定义控件**。 如果要创建的控件不在可用控件列表中，可以将控件添加到列表中。 有关详细信息，请参阅 [向"数据源"窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

    若要了解如何创建可添加到"数据源"窗口中数据表或对象的控件列表的自定义 Windows Forms **控件，** 请参阅创建支持复杂数据绑定的 Windows [Forms](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)用户控件。

## <a name="set-the-controls-to-be-created-for-data-columns-or-properties"></a>设置要针对数据列或属性创建的控件

在将表示对象的列或属性的项从"数据源"窗口拖动到设计器之前，可以设置要创建的控件。

### <a name="to-set-the-controls-to-be-created-for-columns-or-properties"></a>设置要针对列或属性创建的控件

1. 请确保 **WPF 设计器** 或 Windows **窗体** 设计器已打开。

2. 在" **数据源"** 窗口中，展开所需的表或对象以显示其列或属性。

3. 选择要创建控件的每个列或属性。

4. 单击列或属性的下拉菜单，然后选择在将项拖动到设计器时要创建的控件。

     可用控件的列表取决于已打开的设计器、项目面向的 .NET 版本，以及已添加到工具箱 的数据绑定的自定义 **控件**。 如果要创建的控件位于可用控件列表中，可以将该控件添加到列表中。 有关详细信息，请参阅 [向"数据源"窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

     若要了解如何创建可添加到"数据源"窗口中数据列或属性的控件列表的自定义控件，请参阅创建支持简单数据绑定 的[Windows Forms](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)用户控件。

     如果不想为列或属性创建控件，请在下拉菜单中选择"无"。  如果要将父表或对象拖动到设计器，但不希望包含特定列或属性，则此方法很有用。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
