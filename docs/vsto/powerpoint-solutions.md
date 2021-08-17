---
title: PowerPoint解决方案
description: 了解Visual Studio提供了可用于创建 Microsoft VSTO 外接程序的项目PowerPoint。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], PowerPoint
- templates [Office development in Visual Studio], PowerPoint
- solutions [Office development in Visual Studio], PowerPoint
- projects [Office development in Visual Studio], PowerPoint
- PowerPoint [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], PowerPoint
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 97cec1fe5e1954ff04c56f40e3b0313aa35c2170
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122025896"
---
# <a name="powerpoint-solutions"></a>PowerPoint解决方案
  Visual Studio 提供可用于创建 Microsoft Office PowerPoint 的 VSTO 外接程序的项目模板。 可使用 VSTO 外接程序自动化 PowerPoint、扩展 PowerPoint 功能或自定义 PowerPoint 用户界面 (UI)。

 有关外接程序VSTO，请参阅外接程序VSTO和外接程序的体系结构VSTO[编程](architecture-of-vsto-add-ins.md)。 [](getting-started-programming-vsto-add-ins.md)如果刚开始使用 Microsoft Office 编程，请参阅 &#40;Office[中的Visual Studio&#41;。 ](getting-started-office-development-in-visual-studio.md)

 [!INCLUDE[appliesto_pptallapp](includes/appliesto-pptallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="automate-powerpoint-by-using-the-powerpoint-object-model"></a>使用PowerPoint对象模型自动PowerPoint对象
 PowerPoint 对象模型公开了许多你能用于自动化 PowerPoint 的模型。 这些类型使你能够编写代码来完成常规任务：

- 以编程方式创建演示文稿并设置其格式。

- 从演示文稿添加或删除幻灯片。

- 添加或更改幻灯片上的形状。

  若要从PowerPoint外接程序VSTO对象模型，请使用项目中 `Application` `ThisAddIn` 类的 字段。 `Application`字段返回一[个 Application](/previous-versions/office/developer/office-2010/ff764034(v=office.14))对象，该对象表示当前 PowerPoint。 有关详细信息，请参阅[Program VSTO Add-Ins。](programming-vsto-add-ins.md)

  调入 PowerPoint 对象模型时，将使用 PowerPoint 的主互操作程序集中提供的类型。 该主互操作程序集充当 VSTO 外接程序中的托管代码与 PowerPoint 中的 COM 对象模型之间的桥梁。 主互操作程序集PowerPoint类型在[Microsoft.Office 中定义。互操作。PowerPoint](/previous-versions/office/developer/office-2010/ff763170(v=office.14))命名 空间。 有关主互操作程序集的更多信息，请参阅 Office[解决方案](office-solutions-development-overview-vsto.md)开发概述&#40;VSTO&#41;和Office[互操作程序集](office-primary-interop-assemblies.md)。

## <a name="use-the-powerpoint-object-model-documentation"></a><a name="WordOMDocumentation"></a>使用PowerPoint模型文档
 有关 PowerPoint 对象模型的完整信息，可以参考 PowerPoint 主互操作程序集 (PIA) 引用和 VBA 对象模型引用。

### <a name="primary-interop-assembly-reference"></a>主互操作程序集引用
 PowerPoint PIA 参考文档描述了 PowerPoint 的主互操作程序集中的类型。 本文档可从以下位置获得：PowerPoint [2010 主互操作程序集参考](office-primary-interop-assemblies.md)。

 有关 PowerPoint PIA 设计（例如 PIA 中类和接口之间的差异以及如何实现 PIA 中的事件）详细信息，请参阅 Office 主互操作[程序集中的类和接口概述](/previous-versions/office/developer/office-2010/ff759900(v=office.14))。

### <a name="vba-object-model-reference"></a>VBA 对象模型参考
 VBA 对象模型引用在 PowerPoint 对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息，请参阅 PowerPoint [2010 对象模型参考](/office/vba/api/overview/PowerPoint/object-model)。

 VBA 对象模型引用中的所有对象和成员都对应于 PowerPoint 主互操作程序集 (PIA) 中的类型和成员。 例如，VBA 对象模型引用中的 Presentation 对象对应于 POWERPOINT [](/previous-versions/office/developer/office-2010/ff761925(v=office.14)) PIA 中的 Presentation 类型。 虽然 VBA 对象模型引用提供大多数属性、方法和事件的代码示例，但如果你想要在使用 Visual Studio 创建的 PowerPoint VSTO 外接程序项目中使用它们，则必须将本引用中的 VBA 代码转换成 Visual Basic 或 Visual C#。

## <a name="customize-the-user-interface-of-powerpoint"></a>自定义用户的PowerPoint
 你可以通过以下方式修改 PowerPoint 的 UI。

|任务|更多信息|
|----------|--------------------------|
|创建自定义任务窗格。|[自定义任务窗格](custom-task-panes.md)|
|向功能区添加自定义选项卡。|[功能区概述](ribbon-overview.md)|
|向功能区上的内置选项卡添加自定义组。|[如何：自定义内置选项卡](how-to-customize-a-built-in-tab.md)|

 有关自定义应用程序和其他应用程序PowerPoint UI Microsoft Office，请参阅 Office [UI 自定义](office-ui-customization.md)。

## <a name="see-also"></a>请参阅
- [演练：为VSTO创建第一个PowerPoint](walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)
- [外接程序VSTO编程入门](getting-started-programming-vsto-add-ins.md)
- [Office解决方案开发概述&#40;VSTO&#41;](office-solutions-development-overview-vsto.md)
- [VSTO 外接程序的体系结构](architecture-of-vsto-add-ins.md)
- [如何：在 Office 创建Visual Studio](how-to-create-office-projects-in-visual-studio.md)
- [程序VSTO外接程序](programming-vsto-add-ins.md)
- [在解决方案中Office代码](writing-code-in-office-solutions.md)
- [Office主互操作程序集](office-primary-interop-assemblies.md)
- [OfficeUI 自定义](office-ui-customization.md)
- [PowerPoint 2010 Office 开发](/previous-versions/office/developer/office-2010/ff604967(v=office.14))
