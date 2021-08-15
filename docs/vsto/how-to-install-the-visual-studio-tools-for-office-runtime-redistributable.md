---
title: 如何：安装Visual Studio Tools for Office可再发行组件
description: 了解如何安装 Microsoft Visual Studio 2010 Tools for Office Runtime Redistributable。
titleSuffix: ''
ms.custom: seodec18, SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office runtime [Office development in Visual Studio]
- installing Office development tools in Visual Studio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 8850259e152bcd88fe1b20d9db9a9dd0ed1b3e29eb64d08d58148ef0a3983559
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121351936"
---
# <a name="how-to-install-the-visual-studio-tools-for-office-runtime-redistributable"></a>如何：安装Visual Studio Tools for Office可再发行组件
  必须在Visual Studio开发人员工具创建的Office计算机上安装适用于 Office Microsoft Office 运行时的 2010 工具 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 安装 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 Microsoft Office 时会自动安装运行时。 有关详细信息，请参阅 Visual Studio Tools for Office[安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)。

[!include[Add-ins note](includes/addinsnote.md)]

 在以下情况，你可能需要按照手动安装说明操作：

- 需要在服务器上安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。 例如，希望使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类来管理服务器上的文档级解决方案。

- 需要在已安装 Office 解决方案的所有其他先决条件的计算机上安装运行时。

    > [!NOTE]
    > 若要安装 .NET Framework 和 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]，你必须是开发计算机上的管理员。

## <a name="to-install-the-visual-studio-tools-for-office-runtime"></a>安装 Visual Studio Tools for Office runtime

1. 安装 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本。

    - 若要下载 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ，请参阅[Microsoft .NET Framework 4 (Web 安装程序) 。 ](https://www.microsoft.com/download/details.aspx?id=17851)

    - 若要下载 [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)] ，请参阅[Microsoft .NET Framework 4 客户端配置文件 (Web 安装程序) 。 ](https://www.microsoft.com/download/details.aspx?id=17113)

    - 若要下载 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] ，请参阅[Microsoft .NET Framework 4.5。](https://www.microsoft.com/download/details.aspx?id=30653)

2. 运行 *vstor_redist.exe* 安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。

     可以从 Visual Studio [2010 Tools for Office 运行时 下载这些安装文件](https://www.microsoft.com/download/details.aspx?id=56961)。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的先决条件与 .NET Framework 的先决条件相匹配。

     [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 包括语言包。 如果 Windows 安装设置为非英语语言，则可以以 Windows 使用的语言显示运行时消息。 同样，如果最终用户安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]，然后在设置为非英语语言的 Windows 安装上运行你的解决方案，则运行时消息将以与 Windows 相同的语言显示。 在某些情况下，可能需要其他语言包。 例如，如果你的 Windows使用多个语言设置，或者安装 后切换到另一种语言，则你可能需要其他语言包 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 可以在 Microsoft Visual Studio [2010 工具（Microsoft Office 4.0](https://www.microsoft.com/download/details.aspx?id=54246) (运行时语言包）) 语言包。

## <a name="see-also"></a>另请参阅
- [开始&#40;Office开发Visual Studio&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [配置计算机以开发Office解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)
- [如何：配置计算机以开发Office解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [如何：安装Office互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [使用 ServerDocument 类管理服务器上的文档](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [部署Office解决方案](../vsto/deploying-an-office-solution.md)
