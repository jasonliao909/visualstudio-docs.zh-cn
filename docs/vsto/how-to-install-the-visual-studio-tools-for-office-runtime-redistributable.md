---
title: 如何：安装 Visual Studio Tools for Office Runtime 可再发行组件
description: 了解如何安装适用于 Office 运行时可再发行组件的 Microsoft Visual Studio 2010 工具。
titleSuffix: ''
ms.date: 01/25/2022
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
ms.custom: devdivchpfy22
ms.openlocfilehash: 40851fbcb1856176ad571c65bfde741e99b7fd82
ms.sourcegitcommit: 23b0ef3815833426933ff6491271034658683f9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2022
ms.locfileid: "137983835"
---
# <a name="how-to-install-the-visual-studio-tools-for-office-runtime-redistributable"></a>如何：安装 Visual Studio Tools for Office Runtime 可再发行组件

   运行使用中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的 Visual Studio 创建的解决方案的每台计算机都必须安装用于 Office 运行时的 Visual Studio 2010 工具。 安装 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 Microsoft Office 时会自动安装运行时。 有关详细信息，请参阅[Visual Studio Tools for Office 运行时安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)。

[!include[Add-ins note](includes/addinsnote.md)]

 在以下情况下，你可能需要遵循手动安装说明：

- 需要在服务器上安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。

- 需要在已安装 Office 解决方案的所有其他先决条件的计算机上安装运行时。

    > [!NOTE]
    > 若要安装 .NET Framework 和 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]，你必须是开发计算机上的管理员。

## <a name="to-install-the-visual-studio-tools-for-office-runtime"></a>安装 Visual Studio Tools for Office runtime

1. 安装 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本。

    - 若要下载 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ，请参阅[Microsoft .NET Framework 4 (Web 安装程序) ](https://www.microsoft.com/download/details.aspx?id=17851)。

    - 若要下载 [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)] ，请参阅[Microsoft .NET Framework 4 客户端配置文件 (Web 安装程序) ](https://www.microsoft.com/download/details.aspx?id=17113)。

    - 若要下载 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] ，请参阅[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)。

2. 运行 *vstor_redist.exe* 以安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。

     可以从[适用于 Office 运行时的 Visual Studio 2010 工具](https://www.microsoft.com/download/details.aspx?id=56961)下载这些安装程序文件。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的先决条件与 .NET Framework 的先决条件相匹配。

     [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 包括语言包。 如果 Windows 安装设置为非英语语言，则可以以 Windows 使用的语言显示运行时消息。 同样，如果您安装了 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。 然后，在使用非英语语言的 Windows 安装中运行解决方案，运行时消息将以与 Windows 相同的语言显示。 在某些情况下，可能需要更多语言包。 例如，如果 Windows 的副本使用多种语言设置，则可能需要额外的语言包。 或者，你可以在安装 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 后切换到另一种语言。 可以在[Microsoft Office system (4.0 版运行时) 语言包的 Microsoft Visual Studio 2010 工具](https://www.microsoft.com/download/details.aspx?id=54246)中找到语言包。

## <a name="see-also"></a>另请参阅

- [&#40;Visual Studio 中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [将计算机配置为开发 Office 解决方案](../vsto/configuring-a-computer-to-develop-office-solutions.md)
- [如何：将计算机配置为开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)
- [如何：安装 Office 主互操作程序集](../vsto/how-to-install-office-primary-interop-assemblies.md)
- [使用 ServerDocument 类管理服务器上的文档](../vsto/managing-documents-on-a-server-by-using-the-serverdocument-class.md)
- [部署 Office 解决方案](../vsto/deploying-an-office-solution.md)
