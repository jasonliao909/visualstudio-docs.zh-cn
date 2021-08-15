---
title: InfoPath 解决方案
description: 了解如何使用 Visual Studio 为 Microsoft InfoPath 2013 VSTO InfoPath 2010 创建外接程序。
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
ms.openlocfilehash: aafd260434a80d84c192c4c84b5435de4f847310a1e87cddf90f20359e8b4b93
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394131"
---
# <a name="infopath-solutions"></a>InfoPath 解决方案
  Visual Studio 提供了一些项目模板，你可以使用这些模板来创建用于 Microsoft Office InfoPath 2013 和 InfoPath 2010 的 VSTO 外接程序。 InfoPath 在 Office 2016 中不可用。

> [!NOTE]
> 即使已安装 2016 VSTO，仍可以创建 InfoPath Office外接程序。 只需与 Office 2016 并行安装 InfoPath 2013 或 Office 2013。

 [!INCLUDE[appliesto_infoallapp](../vsto/includes/appliesto-infoallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

 InfoPath 的 VSTO 外接程序类似于其他 Microsoft Office 应用程序的 VSTO 外接程序。 这些类型的解决方案包含由应用程序加载的一个程序集。 不管打开了哪个窗体或窗体模板，最终用户都能访问此程序集的功能。 有关外接程序VSTO，请参阅外接程序的VSTO入门和外接程序VSTO[体系结构](../vsto/architecture-of-vsto-add-ins.md)。 [](../vsto/getting-started-programming-vsto-add-ins.md)

> [!NOTE]
> Visual Studio 2015 不包括 Visual Studio 的早期版本中提供的 InfoPath 窗体模板项目。 也无法使用 Visual Studio 2015 打开或编辑用 Visual Studio 的早期版本创建的 InfoPath 窗体模板项目。 但是，可以使用 Visual Studio Tools for Applications 打开和编辑 InfoPath 窗体模板项目。 有关详细信息，请参阅使用[InfoPath 2010 VSTO 2008 项目](/archive/blogs/infopath/working-with-vsto-2008-projects-in-infopath-2010)。

## <a name="automate-infopath-by-using-an-add-in"></a>使用外接程序自动执行 InfoPath
 若要从使用 Visual Studio 中的 Office 开发工具创建的 Office VSTO 外接程序访问 InfoPath 对象模型，请在项目中使用 `Application` 类的 `ThisAddIn` 字段。 `Application` 字段返回 <xref:Microsoft.Office.Interop.InfoPath.Application> 对象，该对象表示 InfoPath 的当前实例。 有关详细信息，请参阅[Program VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

 从外接程序调用 InfoPath 对象模型VSTO，将使用 InfoPath 的主互操作程序集中提供的类型。 该主互操作程序集将作为 VSTO 外接程序中的托管代码和 InfoPath 中的 COM 对象模型之间的桥梁。 InfoPath 主互操作程序集中的所有类型都是在 <xref:Microsoft.Office.Interop.InfoPath> 命名空间中定义的。 有关 InfoPath 主互操作程序集的信息，请参阅关于 Microsoft Office [InfoPath 主互操作程序集](/office/client-developer/infopath/external-automation/about-the-microsoft-office-infopath-primary-interop-assembly)。 有关主互操作程序集的一般详细信息，请参阅 Office[解决方案](../vsto/office-solutions-development-overview-vsto.md)开发概述 &#40;VSTO&#41;Office[主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

## <a name="customize-the-user-interface-of-infopath-by-using-an-add-in"></a>使用外接程序自定义 InfoPath 的用户界面
 为 InfoPath VSTO外接程序时，有几个不同的 UI 自定义选项。 下表列出了其中一些选项。

|任务|更多信息|
|----------|--------------------------|
|创建自定义任务窗格。|[自定义任务窗格](../vsto/custom-task-panes.md)|
|向 InfoPath 的功能区中添加自定义选项卡。|[自定义 InfoPath 的功能区](../vsto/customizing-a-ribbon-for-infopath.md)|

 有关自定义 InfoPath 和其他应用程序 UI Microsoft Office，请参阅自定义 Office [UI。](../vsto/office-ui-customization.md)

## <a name="see-also"></a>另请参阅
- [关于 Microsoft Office InfoPath 主互操作程序集](/office/client-developer/infopath/external-automation/about-the-microsoft-office-infopath-primary-interop-assembly)
- [外接程序VSTO编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)
- [在解决方案中Office代码](../vsto/writing-code-in-office-solutions.md)
- [Office主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [开发中的 InfoPath 2010 Office开发](/previous-versions/office/developer/office-2010/ff604966(v=office.14))