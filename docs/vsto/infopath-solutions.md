---
title: InfoPath 解决方案
description: 了解如何使用 Visual Studio 为 Microsoft InfoPath 2013 和 InfoPath 2010 创建 VSTO 外接程序。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], InfoPath
- templates [Office development in Visual Studio], InfoPath
- InfoPath [Office development in Visual Studio]
- Office development in Visual Studio, InfoPath solutions
- projects [Office development in Visual Studio], InfoPath
- Office solutions [Office development in Visual Studio], InfoPath
- Office projects [Office development in Visual Studio], InfoPath
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 22d8a0bf0ec927cff6499a8401ce0601add22f02
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122155691"
---
# <a name="infopath-solutions"></a>InfoPath 解决方案
  Visual Studio 提供了一些项目模板，你可以使用这些模板来创建用于 Microsoft Office InfoPath 2013 和 InfoPath 2010 的 VSTO 外接程序。 InfoPath 在 Office 2016 中不可用。

> [!NOTE]
> 即使已安装了 Office 2016，你仍可创建用于 InfoPath 的 VSTO 外接程序。 只需与 Office 2016 并行安装 InfoPath 2013 或 Office 2013。

 [!INCLUDE[appliesto_infoallapp](../vsto/includes/appliesto-infoallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 InfoPath 的 VSTO 外接程序类似于其他 Microsoft Office 应用程序的 VSTO 外接程序。 这些类型的解决方案包含由应用程序加载的一个程序集。 不管打开了哪个窗体或窗体模板，最终用户都能访问此程序集的功能。 有关 VSTO 外接程序的详细信息，请参阅 VSTO 外接程序的[VSTO 外](../vsto/getting-started-programming-vsto-add-ins.md)接程序和[体系结构](../vsto/architecture-of-vsto-add-ins.md)。

> [!NOTE]
> Visual Studio 2015 不包括 Visual Studio 的早期版本中提供的 InfoPath 窗体模板项目。 也无法使用 Visual Studio 2015 打开或编辑用 Visual Studio 的早期版本创建的 InfoPath 窗体模板项目。 但是，可以使用 Visual Studio Tools for Applications 打开和编辑 InfoPath 窗体模板项目。 有关详细信息，请参阅[使用 InfoPath 2010 中的 VSTO 2008 项目。](/archive/blogs/infopath/working-with-vsto-2008-projects-in-infopath-2010)

## <a name="automate-infopath-by-using-an-add-in"></a>使用外接程序实现 InfoPath 自动化
 若要从使用 Visual Studio 中的 Office 开发工具创建的 Office VSTO 外接程序访问 InfoPath 对象模型，请在项目中使用 `Application` 类的 `ThisAddIn` 字段。 `Application` 字段返回 <xref:Microsoft.Office.Interop.InfoPath.Application> 对象，该对象表示 InfoPath 的当前实例。 有关详细信息，请参阅[Program VSTO 加载项](../vsto/programming-vsto-add-ins.md)。

 从 VSTO 外接程序调入 InfoPath 对象模型时，将使用在 infopath 的主互操作程序集中提供的类型。 该主互操作程序集将作为 VSTO 外接程序中的托管代码和 InfoPath 中的 COM 对象模型之间的桥梁。 InfoPath 主互操作程序集中的所有类型都是在 <xref:Microsoft.Office.Interop.InfoPath> 命名空间中定义的。 有关 infopath 主互操作程序集的详细信息，请参阅[关于 Microsoft Office infopath 主互操作程序集](/office/client-developer/infopath/external-automation/about-the-microsoft-office-infopath-primary-interop-assembly)。 有关主互操作程序集的一般详细信息，请参阅[Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)和[Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

## <a name="customize-the-user-interface-of-infopath-by-using-an-add-in"></a>使用外接程序自定义 InfoPath 的用户界面
 当你为 InfoPath 创建 VSTO 外接程序时，你有多个不同的 UI 自定义选项。 下表列出了其中一些选项。

|任务|更多信息|
|----------|--------------------------|
|创建自定义任务窗格。|[自定义任务窗格](../vsto/custom-task-panes.md)|
|向 InfoPath 的功能区中添加自定义选项卡。|[自定义 InfoPath 功能区](../vsto/customizing-a-ribbon-for-infopath.md)|

 有关自定义 InfoPath 和其他 Microsoft Office 应用程序的 ui 的详细信息，请参阅[Office UI 自定义](../vsto/office-ui-customization.md)。

## <a name="see-also"></a>请参阅
- [关于 Microsoft Office InfoPath 主互操作程序集](/office/client-developer/infopath/external-automation/about-the-microsoft-office-infopath-primary-interop-assembly)
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [Office 开发中的 InfoPath 2010](/previous-versions/office/developer/office-2010/ff604966(v=office.14))