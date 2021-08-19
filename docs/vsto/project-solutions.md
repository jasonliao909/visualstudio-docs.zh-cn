---
title: Project 解决方案
description: 了解如何使用 VSTO 外接程序自动执行 Project、扩展 Project 功能，或 (UI) 自定义 Project 用户界面。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [Office development in Visual Studio], Project
- Office solutions [Office development in Visual Studio], Project
- Project [Office development in Visual Studio]
- templates [Office development in Visual Studio], Project
- Office projects [Office development in Visual Studio], Project
- solutions [Office development in Visual Studio], Project
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6d03ff38fbbf4084c8dd60738b2d5340d53638a1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115039"
---
# <a name="project-solutions"></a>Project 解决方案
  [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 提供可用于创建 Microsoft Office Project 的 VSTO 外接程序的项目模板。 VSTO 外接程序可用于自动运行项目、扩展项目功能或自定义项目用户界面 (UI)。

 有关 VSTO 外接程序的详细信息，请参阅 VSTO 外接程序的[VSTO 外](../vsto/getting-started-programming-vsto-add-ins.md)接程序和[体系结构](../vsto/architecture-of-vsto-add-ins.md)。如果不熟悉如何与 Microsoft Office 进行编程，请参阅[Visual Studio&#41;中的 Office 开发入门 &#40;](../vsto/getting-started-office-development-in-visual-studio.md)。

 [!INCLUDE[appliesto_projallapp](../vsto/includes/appliesto-projallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="automate-project-by-using-the-project-object-model"></a>使用项目对象模型实现项目自动化
 项目对象模型公开了许多可用于实现项目自动化的类型。 可使用这些类型编写代码来完成常规任务，例如以编程方式创建和修改项目中的任务。

 若要从 VSTO 外接程序访问 Project 对象模型，请使用 `Application` `ThisAddIn` 项目中类的字段。 `Application`字段返回 `Microsoft.Office.Interop.MsProject.Application` 对象，该对象表示 Project 的当前实例。 有关详细信息，请参阅[Program VSTO 加载项](../vsto/programming-vsto-add-ins.md)。

 调入项目对象模型时，将使用项目的主互操作程序集中提供的类型。 该主互操作程序集将作为 VSTO 外接程序中的托管代码和项目中的 COM 对象模型之间的桥梁。 项目主互操作程序集中的所有类型都在 `Microsoft.Office.Interop.MSProject` 命名空间中定义。 有关主互操作程序集的详细信息，请参阅 VSTO&#41;和[Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md) [Office 解决方案开发概述 &#40;](../vsto/office-solutions-development-overview-vsto.md) 。

## <a name="use-the-project-object-model-documentation"></a>使用项目对象模型文档
 有关项目对象模型的完整信息，可以参考项目 VBA 对象模型引用。 VBA 对象模型引用在项目对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息，请参阅[Project 对象模型引用](/office/vba/api/project.object)。

 VBA 对象模型引用中的所有对象和成员都对应于项目主互操作程序集 (PIA) 中的类型和成员。 例如，VBA 对象模型引用中的 Calendar 对象对应于 `Microsoft.Office.Interop.MSProject.Calendar` Project PIA 中的类型。 虽然 VBA 对象模型引用提供了大多数属性、方法和事件的代码示例，但如果要在使用 Visual Studio 创建的 Project VSTO 外接程序项目中使用它们，则必须将本引用中的 VBA 代码转换为 Visual Basic 或 Visual c #。

> [!NOTE]
> 此时，没有任何项目主互操作程序集的参考文档。

### <a name="infrastructure-types-in-the-project-primary-interop-assembly"></a>项目主互操作程序集中的基础结构类型
 编写使用项目 PIA 的代码时，您可能会注意到许多类型在 VBA 参考中都未涉及。 这些附加类型可以帮助将项目的基于 COM 的对象模型中的对象转换为托管代码，而不是在代码中直接使用。

 有关详细信息，请参阅[Office 主互操作程序集中的类和接口的概述](/previous-versions/office/office-12/ms247299(v=office.12))。

## <a name="customize-the-user-interface-of-project"></a>自定义项目的用户界面
 可以通过下列方式来自定义项目 UI：

|任务|更多信息|
|----------|--------------------------|
|向项目的功能区添加自定义选项卡|[功能区概述](../vsto/ribbon-overview.md)|

 有关自定义 Project 和其他 Microsoft Office 应用程序的 ui 的详细信息，请参阅[Office UI 自定义](../vsto/office-ui-customization.md)。

## <a name="see-also"></a>请参阅
- [演练：创建你的第一个项目 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [Office 开发中的 Project 2010 和 Project Server 2010](/previous-versions/office/developer/office-2010/ee758031(v=office.14))
