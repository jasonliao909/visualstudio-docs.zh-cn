---
title: 将Office解决方案迁移到 .NET Framework 4 或更高版本
description: 了解如何将 Office 解决方案迁移到 .NET Framework 4 或更高版本，以便项目继续工作。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.Project.TargetFrameworkWarning
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 7685fbcddd4b903784cbd5e936376842630f4641c6c96ca74add1d33af1dc72c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121226149"
---
# <a name="migrate-office-solutions-to-the-net-framework-4-or-later"></a>将Office解决方案迁移到 .NET Framework 4 或更高版本
  如果 Office 项目的目标框架从早期版本的 .NET Framework 更改为 或更高版本，可能需要执行一些额外的步骤才能继续在开发和最终用户计算机上运行 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 解决方案。 有关详细信息，请参阅运行迁移到 Office 4 或 .NET Framework [4.5 .NET Framework项目所需的更改](../vsto/required-changes-to-run-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。

 此外，可能无法再编译该项目。 对于不同版本的 .NET Framework，Office 项目的一些功能具有不同的编程模型。 当 Office 项目的目标框架从 .NET Framework 的早期版本更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本时，必须对项目进行以下代码更改：

- [更新Excel 4 或 .NET Framework 4.5 的 .NET Framework 和 Word 项目](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

- [更新迁移到 Office 4 或 .NET Framework 4.5 的.NET Framework功能区自定义项](update-ribbon-customizations-in-office-projects-to-migrate-to-dotnet-framework-4-or-4-5.md)

- [更新迁移到 Outlook 4 或 .NET Framework 4.5 .NET Framework窗体区域](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

  当从 Visual Studio 的早期版本升级该项目时，Office 项目的目标框架将更改。 有关详细信息，请参阅[升级和迁移Office解决方案](../vsto/upgrading-and-migrating-office-solutions.md)。

  若要详细了解为什么 Office 项目中某些功能在面向 或更高版本时具有不同的编程模型，请参阅针对 .NET Framework 4 或 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] .NET Framework [4.5](../vsto/changes-to-the-design-of-office-projects-that-target-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)和 Visual Studio Tools for Office 运行时概述 的 Office 项目的设计[更改](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

## <a name="see-also"></a>请参阅
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
- [如何：面向 .NET Framework 的某个版本](../ide/visual-studio-multi-targeting-overview.md)
- [排查解决方案Office错误](../vsto/troubleshooting-errors-in-office-solutions.md)
- [对解决方案中的错误Office支持](../vsto/additional-support-for-errors-in-office-solutions.md)
