---
title: VSTO 外接程序编程入门
description: 了解如何使用 VSTO 外接程序自动 Microsoft Office 应用程序、扩展应用程序的功能以及自定义应用程序的用户界面。
ms.custom: SEO-VS-2020
ms.date: 04/28/2021
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.Outlook
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], getting started
- add-ins [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 1757dd6042536b6a042e67a8b3dcd9b12a2ea758
ms.sourcegitcommit: 9cb0097c33755a3e5cbadde3b0a6e9e76cee727d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/13/2021
ms.locfileid: "109848287"
---
# <a name="get-started-programming-vsto-add-ins"></a>VSTO 外接程序编程入门
> [!IMPORTANT]
> VSTO 依赖于 [.NET Framework](https://docs.microsoft.com/dotnet/framework/get-started/overview)。 COM 外接程序也可以用 .NET Framework 来编写。 Office 外接程序不能用 [.Net Core 和 .net 5 +](https://docs.microsoft.com/dotnet/core/dotnet-five)来创建，最新版本的 .net。 这是因为 .NET Core/.NET 5 + 无法在同一进程中与 .NET Framework 一起使用，并且可能会导致加载项加载失败。 你可以继续使用 .NET Framework 来编写适用于 Office 的 VSTO 和 COM 外接程序。 Microsoft 不会将 VSTO 或 COM 外接程序平台更新为使用 .NET Core 或 .NET 5 +。 你可以利用 .NET Core 和 .NET 5 + （包括 ASP.NET Core）来创建 [Office Web 外接程序](https://docs.microsoft.com/office/dev/add-ins/overview/office-add-ins)的服务器端。

  你可以使用 VSTO 外接程序来实现 Microsoft Office 应用程序自动化、扩展应用程序的功能，以及自定义应用程序的用户界面 (UI)。 有关 VSTO 外接程序如何与可以使用 Visual Studio 创建的其他类型的 Office 解决方案进行比较的信息，请参阅 [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="create-vsto-add-in-projects"></a>创建 VSTO 外接程序项目
 使用 " **新建项目** " 对话框中的一个 vsto 外接程序项目模板创建 vsto 外接程序项目。 这些模板包括所需程序集引用和项目文件。 Visual Studio 为 Office 中的大多数应用程序提供 VSTO 外接程序项目模板。

 有关如何创建 VSTO 外接程序项目的详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。 有关项目模板的详细信息，请参阅 [Office 项目模板概述](../vsto/office-project-templates-overview.md)。

## <a name="develop-vsto-add-in-projects"></a>开发 VSTO 外接程序项目
 创建 VSTO 外接程序项目时，Visual Studio 会自动在 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] c # ) 代码文件的) 或 *ThisAddIn* (中创建 ThisAddIn (。 此文件包含 `ThisAddIn` 类，该类为 VSTO 外接程序提供基础。 在加载或卸载 VSTO 外接程序时，可以使用此类的成员运行代码，以访问主机应用程序的对象模型，以及扩展应用程序的功能。 有关详细信息，请参阅 [PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

## <a name="automate-applications-by-using-the-object-models"></a>使用对象模型自动执行应用程序
 Microsoft Office 应用程序的对象模型公开许多类型，可在 VSTO 外接程序中依据这些类型进行编程。 可以使用这些类型来实现应用程序自动化。 例如，可以通过编程方式在 Outlook 中创建和发送电子邮件，也可以在 Word 中打开文档和添加内容。 若要详细了解如何在代码中访问主机应用程序的对象模型，请参阅[Program VSTO Add-Ins。](../vsto/programming-vsto-add-ins.md)

 有关特定 Microsoft Office 应用程序的对象模型的详细信息，请参阅以下主题：

- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)

- [Word 对象模型概述](../vsto/word-object-model-overview.md)

- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)

- [InfoPath 解决方案](../vsto/infopath-solutions.md)

- [PowerPoint 解决方案](../vsto/powerpoint-solutions.md)

- [项目解决方案](../vsto/project-solutions.md)

- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)

## <a name="customize-the-user-interface-of-applications"></a>自定义应用程序的用户界面
 使用 VSTO 外接程序自定义主机应用程序的 UI 有多种方式：

- 对于 Excel 和 Word，可以向文档中添加托管控件。 有关详细信息，请参阅在 [VSTO](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)外接程序中运行时扩展 Word 文档和 Excel 工作簿。

- 如果应用程序支持功能区，则你可以自定义它。 有关详细信息，请参阅功能 [区概述](../vsto/ribbon-overview.md)。

- 如果应用程序支持自定义任务窗格，则你可以创建它。 有关详细信息，请参阅自定义 [任务窗格](../vsto/custom-task-panes.md)。

- 对于 Outlook，你可以创建自定义窗体区域。 有关详细信息，请参阅创建 [Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

- 对于所有 Microsoft Office 应用程序，可以在 VSTO 外接程序中显示 Windows 窗体。

  若要详细了解如何自定义应用程序 UI Microsoft Office，请参阅 [Office UI 自定义](../vsto/office-ui-customization.md)。

## <a name="next-steps"></a>后续步骤
 若要了解如何创建 VSTO 外接程序，请参阅下面的演练：

- [演练：创建适用于 Excel 的第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)

- [演练：创建第一个适用于 Outlook Add-In VSTO 应用](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)

- [演练：为 PowerPoint 创建第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)

- [演练：为项目创建第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)

- [演练：为 Word 创建第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)

  这些演练介绍 Visual Studio 中的 Office开发工具和 VSTO 外接程序的编程模型。

  有关指导你完成 Office 项目中某些常见任务的主题列表，请参阅 [office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)。

## <a name="see-also"></a>另请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [开始 &#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
