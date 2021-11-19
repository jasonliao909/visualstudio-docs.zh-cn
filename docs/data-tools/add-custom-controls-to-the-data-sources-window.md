---
title: 向“数据源”窗口添加自定义控件
description: 向 Visual Studio 中的“数据源”窗口添加自定义控件。 自定义可绑定控件列表。 添加关联控件。
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.datasource.howtoaddcustomcontrol
helpviewer_keywords:
- Data Sources Window, adding controls
- controls [Visual Studio], adding to Data Sources Window
- DefaultBindingPropertyAttribute class, using
- LookupBindingPropertiesAttribute class, using
- ComplexBindingPropertiesAttribute class, using
- Data Sources Window, selecting controls
ms.assetid: 8c43e7d2-ba94-4d9b-96de-3aa971955afd
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.openlocfilehash: 2b29026eb9242dae0526f6022658f65c4a7b0a76
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601239"
---
# <a name="add-custom-controls-to-the-data-sources-window"></a>向“数据源”窗口添加自定义控件

将项从“数据源”窗口拖动到设计图面以创建数据绑定控件时，可以选择创建的控件类型。 窗口中的每个项都有一个下拉列表，其中显示可选控件。 与每个项关联的控件集由项的数据类型决定。 如果列表中未显示你要创建的控件，可以按照本主题中的说明将该控件添加到列表中。

若要详细了解如何为“数据源”窗口中的项选择要创建的数据绑定控件，请参阅[设置从“数据源”窗口拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

## <a name="customize-the-bindable-controls-list"></a>自定义可绑定控件列表

若要为“数据源”窗口中具有特定数据类型的项添加或删除可用控件列表中的控件，请执行以下步骤。

### <a name="to-select-the-controls-to-be-listed-for-a-data-type"></a>选择要为某一数据类型列出的控件

1. 确保已打开 WPF 设计器或 Windows 窗体设计器。

2. 在“数据源”窗口中，单击添加到窗口的数据源中的项，然后单击该项的下拉菜单。

   > [!TIP]
   > 如果“数据源”窗口未打开，通过选择“查看” > “其他窗口” > “数据源”将其打开  。

3. 在下拉菜单中，单击“自定义”。 此时会打开以下对话框之一：

    - 如果已打开 Windows 窗体设计器，则会打开“选项”对话框的“数据 UI 自定义”页  。 有关详细信息，请参阅[数据 UI 自定义选项对话框](../ide/reference/options-windows-forms-designer-data-ui-customization.md)。

    - 如果已打开 WPF 设计器，则会打开“自定义控件绑定”对话框 。

4. 在对话框中，从“数据类型”下拉列表中选择数据类型。

    - 若要自定义表格或对象的控件列表，请选择“[列表]”。

    - 若要为表的列或对象的属性自定义控件列表，请选择基础数据存储中的列或属性的数据类型。

    - 若要自定义控件列表以显示具有用户定义形状的数据对象，请选择“[其他]”。 例如，如果应用程序的自定义控件显示特定对象的多个属性中的数据，请选择“[其他]”。

5. 在“关联控件”框中，选择要为所选数据类型提供的每个控件，或清除要从列表中删除的任何控件选项。

    > [!NOTE]
    > 如果“关联控件”框中未显示要选择的控件，则必须将该控件添加到列表中。 有关详细信息，请参阅[添加关联控件](#add-associated-controls)。

6. 单击 **“确定”** 。

7. 在“数据源”窗口中，单击刚与一个或多个控件关联的数据类型的项，然后单击该项的下拉菜单。

     在“关联控件”框中选择的控件现在显示在项的下拉菜单中。

## <a name="add-associated-controls"></a>添加关联控件

如果要将控件与数据类型相关联，但“关联控件”框中未显示该控件，则必须将该控件添加到列表中。 该控件必须位于当前解决方案或引用程序集中。 它还必须在“工具箱”中可用，并且具有可指定控件数据绑定行为的属性。

将控件添加到关联控件列表：

1. 右键单击“工具箱”并选择“选择项”，将所需控件添加到“工具箱”  。

     控件必须具有以下属性之一：

    |属性|说明|
    |---------------|-----------------|
    |<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|在显示数据的单个列（或属性）的简单控件上实现此属性，例如 <xref:System.Windows.Forms.TextBox>。|
    |<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|在显示数据的列表（或表格）的控件上实现此属性，例如 <xref:System.Windows.Forms.DataGridView>。|
    |<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|在显示数据的列表（或表格）且需要显示单个列或属性的控件上实现此属性，例如 <xref:System.Windows.Forms.ComboBox>。|

2. 对于 Windows 窗体，在“选项”对话框中，打开“数据 UI 自定义”页 。 或者，对于 WPF，打开“自定义控件绑定”对话框。 有关详细信息，请参阅[自定义数据类型的可绑定控件列表](#customize-the-bindable-controls-list)。

3. 在“关联控件”框中，应显示刚添加到“工具箱”中的控件 。

    > [!NOTE]
    > 仅位于当前解决方案或引用程序集中的控件可添加到关联控件列表。 （控件还必须实现上表中的数据绑定属性之一。）若要将数据绑定到“数据源”窗口中不可用的自定义控件，请将控件从“工具箱”拖动到设计图面，然后将要绑定的项从“数据源”窗口拖动到控件上 。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [数据 UI 自定义选项对话框](../ide/reference/options-windows-forms-designer-data-ui-customization.md)
