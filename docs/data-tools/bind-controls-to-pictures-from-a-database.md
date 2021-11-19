---
title: 将控件绑定到数据库中的图片
description: 使用“数据源”窗口将数据库中的图像绑定到 Visual Studio 应用程序中的控件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- images [Visual Basic], displaying on Windows Forms
- data binding [Windows Forms], pictures
- images [Visual Basic], data binding
- pictures, data binding
- pictures, dragging from Data Sources window
- Data Sources Window, setting controls to display images
- PictureBox control [Windows Forms], data binding
- images [Visual Basic], dragging from Data Sources window
ms.assetid: 9748815e-3556-49e8-86b1-c6aa593c6163
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: f1f1db5a2d98b6e55b0da97e7550bc33698ff072
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601226"
---
# <a name="bind-controls-to-pictures-from-a-database"></a>将控件绑定到数据库中的图片

你可使用“数据源”窗口将数据库中的图像绑定到应用程序中的控件。 例如，可将图像绑定到 WPF 应用程序中的 <xref:System.Windows.Controls.Image> 控件，或者绑定到 Windows 窗体应用程序中的 <xref:System.Windows.Forms.PictureBox> 控件。

数据库中的图片通常以字节数组的形式存储。 对于“数据源”窗口中以字节数组形式存储的项，其控件类型默认设置为“无”，因为从简单的字节数组到大型应用程序的可执行文件都可以包含在字节数组中 。 若要在代表图像的“数据源”窗口中为字节数组项创建数据绑定控件，必须选择要创建的控件。

下面的过程假设已使用绑定到图像的项填充“数据源”窗口。

## <a name="to-bind-a-picture-in-a-database-to-a-control"></a>将数据库中的图片绑定到控件

1. 确保在 WPF 设计器或 Windows 窗体设计器中打开要添加控件的设计图面。

2. 在“数据源”窗口中，展开所需的表或对象以显示其列或属性。

   > [!TIP]
   > 如果“数据源”窗口未打开，通过选择“查看” > “其他窗口” > “数据源”将其打开   。

3. 选择包含图像数据的列或属性，并从其下拉控件列表中选择以下控件之一：

    - 如果 WPF 设计器打开，选择“图像”。

    - 如果 Windows 窗体设计器打开，选择“PictureBox”。

    - 此外，也可选择另一个支持数据绑定并可显示图像的控件。 如果要使用的控件不在可用控件列表中，则可将其添加到列表中，然后再选中它。 有关详细信息，请参阅[向“数据源”窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
