---
title: '如何：向 Backstage 视图添加控件 '
description: 了解如何使用功能区设计器将控件添加到单击"文件"选项卡时打开的菜单。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- customizing the Ribbon, menus
- controls, Ribbon
- menus, customizing
- Microsoft Office Button
- custom Ribbon, menus
- Ribbon, customizing
- Office button
- Ribbon, menus
- Microsoft Office Menu
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6ce9a1bda7f828a71fe6128d034d7a81dbb5e678541c3ebac06b3f3214259fec
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121424133"
---
# <a name="how-to-add-controls-to-the-backstage-view"></a>如何：向 Backstage 视图添加控件
  可以使用功能区设计器将控件添加到单击"文件"选项卡时打开 **的** 菜单。运行应用程序时，添加到"文件"选项卡 **的控件将显示** 名为 **"外接程序"的组**。

 不能在控件中通过使用功能区设计器在内置控件之前或之后Visual Studio。 内置控件是已出现在 Backstage 视图中的控件。 如果要将控件定位在内置控件之前或之后，则必须使用功能区 XML。 有关功能区和 **XML () ，** 请参阅 [功能区 XML](../vsto/ribbon-xml.md)。 有关自定义 Backstage 视图的信息，请参阅开发人员的[Office 2010 Backstage](/previous-versions/office/developer/office-2010/ee691833(v=office.14))视图简介和为开发人员自定义[Office 2010 Backstage 视图](/previous-versions/office/developer/office-2010/ee815851(v=office.14))。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-add-controls-to-backstage-view"></a>将控件添加到 Backstage 视图

1. 打开"功能区"中的设计视图。

     若要了解如何将功能区添加到 (**设计器)** 项目，请参阅如何 [：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

2. 在功能区设计器中，单击" **文件"** 选项卡。

     将出现一个菜单设计器。 此设计图面不包含任何控件。

3. 从 **"Office"** 的"功能区控件"选项卡 **中，** 将以下任何控件拖动到菜单设计器上：

    - Button

    - CheckBox

    - 库

    - 菜单

    - Separator

    - SplitButton

    - ToggleButton

4. 拖动控件以将它们移动到菜单上的新位置。

## <a name="see-also"></a>另请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
