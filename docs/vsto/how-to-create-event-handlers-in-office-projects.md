---
title: 如何：在项目中创建Office处理程序
description: 了解在 C# 和 C# 中为控件创建默认事件处理程序Visual Basic方法。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Basic [Office development in Visual Studio], event handlers
- event handlers [Office development in Visual Studio]
- Visual C# [Office development in Visual Studio], event handlers
- events [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6a3ef99f7032f3112ec65a110259a2ad7b3af6ba
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122122834"
---
# <a name="how-to-create-event-handlers-in-office-projects"></a>如何：在项目中创建Office处理程序
  有几种方法在 Visual Basic 和 C# 中创建事件处理程序。 在设计视图中，可以通过双击控件来创建控件的默认事件处理程序，或使用"属性"窗口的"事件"窗格为控件上的任何事件创建处理程序。 但是，如果正在"代码"视图中，你可能不希望切换到设计视图事件处理程序。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-an-event-handler-in-visual-basic"></a>在 Visual Basic

1. 从 **代码编辑器** 顶部的"类名"下拉列表中，选择要创建事件处理程序的对象。

    > [!NOTE]
    > 如果要为 或 创建事件处理程序，则必须在"类名"下拉列表中选择" (ThisDocument 事件) 或 (`ThisDocument` `ThisWorkbook` **ThisWorkbook** 事件) "

2. 从 **代码编辑器顶部的** "方法名称"下拉列表中，选择事件。

     Visual Studio创建事件处理程序，将插入点移动到新创建的事件处理程序。 如果事件处理程序已存在，则插入点将移动到现有事件处理程序。

### <a name="to-create-an-event-handler-in-c"></a>在 C 中创建事件处理程序\#

1. 在 类的 **Startup** 事件创建事件委托，方法为键入限定的事件名称，后跟空格，然后键入 **+=** 无空格。 例如：

     `this.<object name>.<event name> +=`

2. 在代码行的末尾，按 TAB 键两次。

     Visual Studio自动完成代码行，创建事件处理程序，将插入点移动到新创建的事件处理程序。

## <a name="see-also"></a>请参阅
- [在解决方案中Office代码](../vsto/writing-code-in-office-solutions.md)
- [演练：针对 NamedRange 控件的事件进行编程](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [生成Office解决方案](../vsto/building-office-solutions.md)
