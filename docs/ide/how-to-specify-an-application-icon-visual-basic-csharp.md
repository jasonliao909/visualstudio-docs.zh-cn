---
title: 如何：指定应用程序图标（Visual Basic、C#）
description: 了解如何使用“图标”属性指定文件资源管理器和 Windows 任务栏针对已编译应用程序所显示的图标。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- icons [Visual Studio], application
- application properties [Visual Studio], icons
- application icons [Visual Studio]
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- dotnet
ms.openlocfilehash: 0c03ae786a3fd748177a776b6f2bc2a2e67cb802
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122109157"
---
# <a name="how-to-specify-an-application-icon-visual-basic-c"></a>如何：指定应用程序图标（Visual Basic、C#）

项目的 `Icon` 属性指定将针对已编译应用程序在文件资源管理器和 Windows 任务栏中显示的图标文件 (.ico)。

`Icon` 属性可以在“项目设计器”的“应用程序”窗格中进行访问；它包含作为资源或内容文件添加到项目中的图标列表。 

> [!NOTE]
> 在设置应用程序的图标属性后，你可能还要设置应用程序中每个“窗口”或“窗体”的 `Icon` 属性。  有关 Windows Presentation Foundation (WPF) 独立应用程序的窗口图标的信息，请参阅 <xref:System.Windows.Window.Icon%2A> 属性。

## <a name="to-specify-an-application-icon"></a>如要指定应用程序图标

1. 在“解决方案资源管理器”中，选择项目节点（而非“解决方案”节点）。 

1. 在菜单栏上，选择“项目” > “属性” 。

1. 当“项目设计器”出现时，选择“应用程序”选项卡。 

1. (Visual Basic)&mdash;在“图标”列表中，选择一个图标 (.ico) 文件 。

    C#&mdash;在“图标”列表附近，选择“\<Browse...>”按钮，然后转到所需图标文件的位置。

## <a name="see-also"></a>请参阅

- [项目设计器的应用程序页 (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)
- [项目设计器的应用程序页 (C#)](../ide/reference/application-page-project-designer-csharp.md)
