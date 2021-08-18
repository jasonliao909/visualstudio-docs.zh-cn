---
title: 外接程序VSTO编程入门
description: 了解如何使用 VSTO 外接程序自动Microsoft Office应用程序、扩展应用程序的功能以及自定义应用程序的用户界面。
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
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 65ccd3385ca33e098eb5cec073ea56fd742e4d65
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122130515"
---
# <a name="get-started-programming-vsto-add-ins"></a>外接程序VSTO编程入门
> [!IMPORTANT]
> VSTO依赖于[.NET Framework。](https://docs.microsoft.com/dotnet/framework/get-started/overview) COM 外接程序也可使用 .NET Framework。 Office无法使用 .NET Core 和[.NET 5+](https://docs.microsoft.com/dotnet/core/dotnet-five)（最新版本的 .NET）创建外接程序。 这是因为 .NET Core/.NET 5+ 不能与同一进程中.NET Framework，并且可能会导致外接程序加载失败。 可以继续使用 .NET Framework 为VSTO和 COM 外接程序编写Office。 Microsoft 不会更新 VSTO COM 外接程序平台以使用 .NET Core 或 .NET 5+。 可以利用 .NET Core 和 .NET 5+（包括 ASP.NET Core）来创建 Web 外接程序 Office[服务器端](https://docs.microsoft.com/office/dev/add-ins/overview/office-add-ins)。

  你可以使用 VSTO 外接程序来实现 Microsoft Office 应用程序自动化、扩展应用程序的功能，以及自定义应用程序的用户界面 (UI)。 有关外接程序VSTO与可以使用 Visual Studio 创建的其他类型的 Office 解决方案相比，请参阅 Office[解决方案开发&#40;VSTO&#41;。 ](../vsto/office-solutions-development-overview-vsto.md)

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="create-vsto-add-in-projects"></a>创建VSTO外接程序项目
 使用VSTO"新建"对话框中的VSTO外接程序项目模板之一创建 **Project项目。** 这些模板包括所需程序集引用和项目文件。 Visual Studio 为 Office 中的大多数应用程序提供 VSTO 外接程序项目模板。

 若要详细了解如何创建 VSTO 外接程序项目，请参阅如何：在 Office[创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md) 有关项目模板详细信息，请参阅Office[模板概述](../vsto/office-project-templates-overview.md)。

## <a name="develop-vsto-add-in-projects"></a>开发VSTO外接程序项目
 创建 VSTO 外接程序项目时，Visual Studio 会在) 中自动创建 *ThisAddIn.vb* (，或在 C#) 代码文件中自动创建 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] *ThisAddIn.cs* (。 此文件包含 `ThisAddIn` 类，该类为外接程序VSTO基础。 在加载或卸载 VSTO 外接程序时，可以使用此类的成员运行代码，以访问主机应用程序的对象模型，以及扩展应用程序的功能。 有关详细信息，请参阅[Program VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

## <a name="automate-applications-by-using-the-object-models"></a>使用对象模型自动执行应用程序
 Microsoft Office 应用程序的对象模型公开许多类型，可在 VSTO 外接程序中依据这些类型进行编程。 可以使用这些类型来实现应用程序自动化。 例如，可以通过编程方式在 Outlook 中创建和发送电子邮件，也可以在 Word 中打开文档和添加内容。 若要详细了解如何在代码中访问主机应用程序的对象模型，请参阅 Program [VSTO Add-Ins。](../vsto/programming-vsto-add-ins.md)

 有关特定 Microsoft Office 应用程序的对象模型的详细信息，请参阅以下主题：

- [Excel对象模型概述](../vsto/excel-object-model-overview.md)

- [Word 对象模型概述](../vsto/word-object-model-overview.md)

- [Outlook对象模型概述](../vsto/outlook-object-model-overview.md)

- [InfoPath 解决方案](../vsto/infopath-solutions.md)

- [PowerPoint解决方案](../vsto/powerpoint-solutions.md)

- [Project解决方案](../vsto/project-solutions.md)

- [Visio对象模型概述](../vsto/visio-object-model-overview.md)

## <a name="customize-the-user-interface-of-applications"></a>自定义应用程序的用户界面
 在外接程序中，有几种不同的方法可以自定义主机VSTO UI：

- 对于 Excel 和 Word，可以向文档中添加托管控件。 有关详细信息，请参阅扩展[Word 文档和Excel运行时VSTO外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

- 如果应用程序支持功能区，则你可以自定义它。 有关详细信息，请参阅功能 [区概述](../vsto/ribbon-overview.md)。

- 如果应用程序支持自定义任务窗格，则你可以创建它。 有关详细信息，请参阅自定义 [任务窗格](../vsto/custom-task-panes.md)。

- 对于 Outlook，你可以创建自定义窗体区域。 有关详细信息，请参阅[创建Outlook区域。](../vsto/creating-outlook-form-regions.md)

- 对于所有 Microsoft Office 应用程序，可以在 VSTO 外接程序中显示 Windows 窗体。

  若要详细了解如何自定义应用程序 UI Microsoft Office，请参阅 Office [UI 自定义](../vsto/office-ui-customization.md)。

## <a name="next-steps"></a>后续步骤
 若要了解如何创建 VSTO 外接程序，请参阅下面的演练：

- [演练：为 VSTO 创建第一个Excel](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)

- [演练：创建第一个VSTO Add-In应用Outlook](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)

- [演练：为VSTO创建第一个PowerPoint](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)

- [演练：为VSTO创建第一个Project](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)

- [演练：为 Word VSTO第一个外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)

  这些演练介绍 Visual Studio 中的 Office开发工具和 VSTO 外接程序的编程模型。

  有关演练项目中的一些常见任务的主题Office，请参阅编程 中的[Office任务](../vsto/common-tasks-in-office-programming.md)。

## <a name="see-also"></a>请参阅
- [如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [开始&#40;Office开发Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [在解决方案中Office代码](../vsto/writing-code-in-office-solutions.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)
