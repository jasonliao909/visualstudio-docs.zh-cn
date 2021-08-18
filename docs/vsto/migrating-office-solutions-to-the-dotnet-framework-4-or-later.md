---
title: 将 Office 解决方案迁移到 .NET Framework 4 或更高版本
description: 了解如何将 Office 解决方案迁移到 .NET Framework 4 或更高版本，以便您的项目可以继续工作。
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
ms.openlocfilehash: 36ad3fa7fb59dcef142030d16dda5f637427a378
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032454"
---
# <a name="migrate-office-solutions-to-the-net-framework-4-or-later"></a>将 Office 解决方案迁移到 .NET Framework 4 或更高版本
  如果 Office 项目的目标框架 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 从 .NET Framework 早期版本更改为或更高版本，则可能需要执行一些其他步骤才能继续运行开发计算机和最终用户计算机上的解决方案。 有关详细信息，请参阅[运行 Office 迁移到 .NET Framework 4 或 .NET Framework 4.5 的项目所需的更改](../vsto/required-changes-to-run-office-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)。

 此外，可能无法再编译该项目。 对于不同版本的 .NET Framework，Office 项目的一些功能具有不同的编程模型。 当 Office 项目的目标框架从 .NET Framework 的早期版本更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本时，必须对项目进行以下代码更改：

- [更新迁移到 .NET Framework 4 或 .NET Framework 4.5 的 Excel 和 Word 项目](../vsto/updating-excel-and-word-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

- [更新迁移到 .NET Framework 4 或 .NET Framework 4.5 Office 项目中的功能区自定义项](update-ribbon-customizations-in-office-projects-to-migrate-to-dotnet-framework-4-or-4-5.md)

- [更新迁移到 .NET Framework 4 或 .NET Framework 4.5 Outlook 项目中的窗体区域](../vsto/updating-form-regions-in-outlook-projects-that-you-migrate-to-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)

  当从 Visual Studio 的早期版本升级该项目时，Office 项目的目标框架将更改。 有关详细信息，请参阅[升级和迁移 Office 解决方案](../vsto/upgrading-and-migrating-office-solutions.md)。

  若要详细了解在面向或更高版本时，Office 项目中的某些功能具有不同的编程模型 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ，请参阅[面向 .NET Framework 4 的 Office 项目的设计更改或 .NET Framework 4.5](../vsto/changes-to-the-design-of-office-projects-that-target-the-dotnet-framework-4-or-the-dotnet-framework-4-5.md)和[Visual Studio Tools for Office 运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)。

## <a name="see-also"></a>请参阅
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [如何：面向 .NET Framework 的某个版本](../ide/visual-studio-multi-targeting-overview.md)
- [排查 Office 解决方案中的错误](../vsto/troubleshooting-errors-in-office-solutions.md)
- [对 Office 解决方案中的错误的其他支持](../vsto/additional-support-for-errors-in-office-solutions.md)
