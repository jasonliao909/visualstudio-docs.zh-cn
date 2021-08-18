---
title: 迁移到 .NET 4.5 Office项目所需的更改
description: 了解如果目标框架从早期版本的版本更改到 .NET Framework 4 或更高版本，则需要对项目所做的更改.NET Framework。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 8b1e3ca556e07e0d4df8a27142a0700fd40e09a2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032220"
---
# <a name="changes-required-for-office-projects-migrated-to-net-45"></a>迁移到 .NET 4.5 Office项目所需的更改

  如果 Office 项目的目标框架从 .NET Framework 的早期版本更改为 或更高版本，则必须执行以下任务以确保解决方案可以在开发计算机和最终用户计算机上 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 运行：

- 删除项目中的 <xref:System.Security.SecurityTransparentAttribute>如果从 Visual Studio 2008 升级它）。

- 在 **Visual Studio** 执行 Clean 命令，以在开发计算机上运行或调试项目。

- 更新项目的 .NET Framework 必备组件。

- 如果以前通过在更改目标框架之前使用 ClickOnce 部署解决方案，则最终用户还必须重新安装该解决方案。

  有关上述每个任务的详细信息，请参阅以下相应章节。

## <a name="remove-the-securitytransparent-attribute-from-projects-that-you-upgrade-from-visual-studio-2008"></a>从 2008 年 8 月升级的项目中删除 SecurityTransparent Visual Studio属性
 如果从 Visual Studio 2008 升级 Office project 项目，且项目的目标框架随后更改为 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则必须从项目中删除 <xref:System.Security.SecurityTransparentAttribute>。 Visual Studio 不会为你自动删除此属性。 如果不删除此属性，则编译项目时将收到一条错误消息。

 有关升级后的项目Visual Studio框架更改为 或 的条件，请参阅升级和迁移Office [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] [解决方案](../vsto/upgrading-and-migrating-office-solutions.md)。

#### <a name="to-remove-the-securitytransparentattribute"></a>若要删除 SecurityTransparentAttribute

1. 在 Visual Studio 中打开项目后，打开 **“解决方案资源管理器”**。

2. 在 C# 的 **“属性”** 节点或在 Visual Basic 的 **“我的项目”** 节点下，双击 AssemblyInfo 代码文件以在代码编辑器中打开它。

    > [!NOTE]
    > 在 Visual Basic 项目中，必须单击 **“解决方案资源管理器”** 中的 **“显示所有文件”** 按钮，才能查看 AssemblyInfo 代码文件。

3. 找到 <xref:System.Security.SecurityTransparentAttribute> 并且将其从文件中删除或注释掉。

    ```vb
    <Assembly: SecurityTransparent()>
    ```

    ```csharp
    [assembly: SecurityTransparent()]
    ```

## <a name="perform-the-clean-command-to-debug-or-run-a-project-on-the-development-computer"></a>执行清理命令，在开发计算机上调试或运行项目
 如果在Office框架更改为 或更高版本之前生成了项目，则必须执行 Clean 命令，然后在目标框架更改后 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 重新生成项目。 如果不执行 **Clean** 命令，则当你尝试调试或运行重定目标项目时， <xref:System.Runtime.InteropServices.COMException> 将收到 。

 有关 Clean 命令 **的更多信息**，请参阅生成Office [解决方案](../vsto/building-office-solutions.md)。

## <a name="update-the-prerequisites-for-deployment"></a>更新部署的先决条件
 将项目Office或更高版本时，还必须在"先决条件 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ".NET Framework中更新相应的先决条件。  否则，ClickOnce 部署或 InstallShield Limited Edition 项目将检查并安装 .NET Framework 的早期版本。

 有关更新部署到最终用户计算机的先决条件的更多信息，请参阅如何：在最终用户计算机上安装必备组件以运行Office[解决方案](/previous-versions/bb608608(v=vs.110))。

## <a name="reinstall-solutions-on-end-user-computers"></a>在最终用户计算机上重新安装解决方案
 如果使用 ClickOnce 部署面向 .NET Framework 3.5 的 Office 解决方案，然后将项目重新定位到 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，则最终用户必须卸载解决方案，然后在发布解决方案后进行重新安装。 如果重新发布重定向的解决方案，并且解决方案在最终用户计算机上更新，则最终用户在运行更新的解决方案时将收到 <xref:System.Runtime.InteropServices.COMException> 。

## <a name="see-also"></a>请参阅
- [将Office解决方案迁移到 .NET Framework 4 或更高版本](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)