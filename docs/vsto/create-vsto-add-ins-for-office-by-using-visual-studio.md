---
title: 使用 Visual Studio 创建 VSTO 外接程序
description: 了解如何使用 Microsoft Office 开发人员工具创建Visual Studio扩展.NET Framework的应用程序Office。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 04/28/2021
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 46330c69b89b297b82ce70d3fb6eb0b7bd7d95df
ms.sourcegitcommit: 42aec4a2ea6dec67dbe4c93bcf0fa1116a4b93d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2021
ms.locfileid: "122981068"
---
# <a name="create-vsto-add-ins-for-office-by-using-visual-studio"></a>使用 Visual Studio 创建 VSTO 外接程序
> [!IMPORTANT]
> VSTO依赖于[.NET Framework。](/dotnet/framework/get-started/overview) COM 外接程序也可使用 .NET Framework。 Office无法使用 .NET Core 和[.NET 5+](/dotnet/core/dotnet-five)（最新版本的 .NET）创建外接程序。 这是因为 .NET Core/.NET 5+ 不能与同一进程中.NET Framework，并且可能会导致外接程序加载失败。 可以继续使用 .NET Framework 为 VSTO 和 COM 外接程序Office。 Microsoft 不会更新 VSTO COM 外接程序平台以使用 .NET Core 或 .NET 5+。 可以利用 .NET Core 和 .NET 5+（包括 ASP.NET Core）来创建 Web 外接程序 Office[服务器端](/office/dev/add-ins/overview/office-add-ins)。

  可以使用 Visual Studio 中的 Microsoft Office 开发人员工具来创建可扩展 Office 的 .NET Framework 应用程序。 这些应用程序也称为“Office 解决方案” 。

 Office 开发人员工具提供了一些功能，可帮助你创建适合于各种业务需求的 Office 解决方案。 这些工具包括项目模板和可视化设计器，前者有助于你通过使用 Visual Basic 或 Visual C# 创建 Office 解决方案，后者有助于你为 Office 解决方案创建自定义用户界面。

[!include[Add-ins note](includes/addinsnote.md)]

 有关开发的最新Office，请参阅 Microsoft Office[开发人员中心](https://developer.microsoft.com/office/docs)。

## <a name="in-this-section"></a>在本节中
- [开始&#40;Office开发Visual Studio&#41;](getting-started-office-development-in-visual-studio.md)

 提供一些链接，这些链接指向有关如何配置开发计算机以创建 Office 解决方案、如何开始创建 Office 解决方案以及 Visual Studio 中的 Office 开发的新增功能的信息。

- [升级和迁移Office解决方案](upgrading-and-migrating-office-solutions.md)

 提供一些链接，这些链接指向有关使用 Visual Studio 早期版本创建的项目的升级过程的信息。

- [解决方案Office体系结构Visual Studio](architecture-of-office-solutions-in-visual-studio.md)

 提供一些链接，这些链接指向有关 Office 解决方案的工作原理的信息，其中包括有关文档级自定义项和 VSTO 外接程序的信息。

- [设计和创建Office解决方案](designing-and-creating-office-solutions.md)

 提供有关如何在 Visual Studio 中创建和配置 Office 项目的信息。

- [开发Office解决方案](developing-office-solutions.md)

 提供有关如何在 Office 解决方案中使用托管代码的信息，其中包括如何自定义 Office 用户界面、使用数据以及解决问题的信息。

- [Excel解决方案](excel-solutions.md)

 提供有关如何实现 Excel 自动化、创建 Excel 解决方案以及了解特定于 Excel 的全球化问题的信息。

- [InfoPath 解决方案](infopath-solutions.md)

 提供有关如何创建 InfoPath 的表单模板和 VSTO 外接程序的信息。

- [Outlook解决方案](outlook-solutions.md)

 提供有关如何实现 Outlook 自动化以及创建 Outlook VSTO 外接程序和窗体区域的信息。

- [PowerPoint解决方案](powerpoint-solutions.md)

 提供有关如何实现 PowerPoint 自动化和创建 PowerPoint VSTO 外接程序的信息。

- [Project解决方案](project-solutions.md)

 提供有关如何在外接程序中Microsoft Office和创建项目VSTO的信息。

- [Visio解决方案](visio-solutions.md)

 提供有关如何实现 Visio 自动化和创建 Visio VSTO 外接程序的信息。

- [Word 解决方案](word-solutions.md)

 提供有关如何实现 Word 自动化和创建 Word 解决方案的信息。

- [生成Office解决方案](building-office-solutions.md)

 提供有关在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中生成 Office 项目和其他类型项目之间的差异的信息。

- [调试Office项目](debugging-office-projects.md)

 提供有关在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中调试 Office 项目和其他类型项目之间的差异的信息。

- [安全Office解决方案](securing-office-solutions.md)

 提供有关 Office 解决方案中安全功能的工作原理的信息。

- [部署 Office 解决方案](deploying-an-office-solution.md)

 提供有关如何让用户使用 Office 解决方案，以及在选择部署方法时要考虑的主要问题的信息。

- [Office开发示例和演练](office-development-samples-and-walkthroughs.md)

 提供指向示例应用程序和主题的链接，这些主题提供有关执行常规任务的分步说明。

- [&#40;Office开发中的一般Visual Studio&#41;](general-reference-office-development-in-visual-studio.md)

 提供有关主互操作程序集Office清单、用户界面元素和错误消息的详细信息的链接。

- [托管参考&#40;Office开发Visual Studio&#41;](managed-reference-office-development-in-visual-studio.md)

 提供指向有关在 Office 项目中使用的针对 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]的 API 命名空间和类型的链接。 有关面向 .NET Framework 3.5 的 Office 项目中使用的命名空间和类型的 API 参考文档，请参阅 Visual Studio 2008 文档中的以下参考部分[：2007](managed-reference-office-development-in-visual-studio.md)系统托管参考 。

- [非托管 API 参考&#40;Office开发Visual Studio&#41;](unmanaged-api-reference-office-development-in-visual-studio.md)

 包含一些链接，这些链接指向有关可以使用 COM 接口执行各种操作（例如加载和卸载 Office 应用程序中托管 VSTO 外接程序）方面的信息。

## <a name="related-sections"></a>相关章节
- [Office开发人员门户Visual Studio开发](https://developer.microsoft.com/office/docs)提供其他资源，例如技术文章、视频和博客。

- [Visual Studio开发人员中心](https://visualstudio.microsoft.com/)提供其他Visual Studio资源，例如技术文章、视频和博客。

- [Microsoft Office MSDN 库的开发部分](/previous-versions/office/office-12/bb726434(v=office.12))MSDN 库的区域，可在其中找到有关为多个版本的 Office (开发解决方案的文章和参考文档，Office使用 Visual Studio) 。

- [应用程序中的应用程序Visual Studio](/previous-versions/h8w79z10(v=vs.140))包含一些主题的链接，这些主题说明如何使用 Visual Studio设计、开发、调试和部署 Web 应用程序、XML Web 服务与传统客户端应用程序。

- [.NET Framework编程Visual Studio](/previous-versions/visualstudio/visual-studio-2010/k1s94fta(v=vs.100))讨论在 .NET Framework 和 Visual C# Visual Basic应用程序开发。
