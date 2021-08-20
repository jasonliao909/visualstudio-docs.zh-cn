---
description: 使用此窗口可查看和更改编辑器和设计器中选中对象的设计时属性和事件。
title: “属性”窗口
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- properties [Visual Studio], Properties Window
- handler functions, Properties window
- handlers, Properties window
- Windows messages
- properties [Visual Studio], setting at design time
- properties [Visual Studio], editing
- Property Browser
- Windows messages, adding message handlers
- Properties window, overrides
- virtual functions, Properties window
- Properties window
ms.assetid: e6e0fa4f-75c4-4a52-af15-281cd61876ca
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 364067fd5661d71ab97f6d30de7ea1db35598e8e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122151140"
---
# <a name="properties-window"></a>“属性”窗口

使用此窗口可查看和更改编辑器和设计器中选中对象的设计时属性和事件。 还可以使用“属性”窗口编辑和查看文件、项目和解决方案属性。 可以在“视图”菜单上找到“属性”窗口。 可以按 F4 打开它，也可以在搜索框中键入“属性”打开。

“属性”窗口可根据特定属性的需要显示不同类型的编辑字段。 这些编辑字段包括编辑框、下拉列表和自定义编辑器对话框的链接。 显示为灰色的属性为只读属性。

## <a name="uielement-list"></a>UIElement 列表

对象名称\
列出当前选择的对象。 只有处于活动状态的编辑器或设计器中的对象是可见的。 选择多个对象时，仅显示所有选定对象的共同属性。

按分类顺序\
按类别列出所选对象的所有属性和属性值。 可以将类别折叠起来以减少可见属性的数量。 折叠或展开类别时，在类别名称的左侧将显示一个加号 (+) 或减号 (-)。 类别按字母顺序列出。

按字母顺序\
所选对象的所有设计时属性和事件按字母顺序排列。 要编辑不灰显的属性，请单击它右侧的单元格并输入更改内容。

属性页\
显示选中项的“属性页”对话框或“项目设计器”。 属性页显示“属性”窗口提供的属性子集、相同属性或属性超集。 使用此按钮查看和编辑与项目的活动配置相关的属性。

属性\
显示对象的属性。 很多对象的事件还可以使用“属性”窗口查看。

按属性源排序\
按源（如继承、应用样式和绑定）对属性进行分组。 仅在设计器中编辑 XAML 文件时可用。

事件\
显示对象的事件。

> [!NOTE]
> 该“属性”窗口工具栏控件仅在 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 项目的上下文中的窗体或控件设计器处于活动状态时可用。 编辑 XAML 文件时，事件将显示在属性窗口的单独选项卡上。

消息\
列出所有 Windows 消息。 允许针对为选定类提供的消息添加或删除指定处理程序函数。

> [!NOTE]
> 该“属性”窗口工具栏控件仅在“类视图”在 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目的上下文中为活动窗口时可用。

重写\
列出选定类的所有虚函数并允许添加或删除重写函数。

> [!NOTE]
> 该“属性”窗口工具栏控件仅在“类视图”在 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目的上下文中为活动窗口时可用。

说明窗格\
显示属性类型和属性的简短说明。 可以使用快捷菜单上的说明命令关闭和打开属性的说明。

> [!NOTE]
> 在设计器中编辑 XAML 文件时，此“属性”窗口工具栏控件不可用。

缩略图视图\
在设计器中编辑 XAML 文件时，显示了当前所选元素的可视表示形式。

搜索\
在设计器中编辑 XAML 文件时提供属性和事件的搜索函数。 搜索框对应于部分单词搜索并在键入时更新搜索结果。

## <a name="see-also"></a>请参阅

- [项目属性引用](../../ide/reference/project-properties-reference.md)
- [自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)
