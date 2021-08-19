---
title: Visual Studio Tools for Office 运行时安装方案
description: 了解如何安装适用于 Office 运行时的 Visual Studio 2010 工具。 本文介绍三种安装方案。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio Tools for Office runtime, installation scenarios
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 110e78b404ef5d25264a0e168bf9b6de5cad5d3c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122082681"
---
# <a name="visual-studio-tools-for-office-runtime-installation-scenarios"></a>Visual Studio Tools for Office 运行时安装方案

  可以通过三种方式安装适用于 Office 运行时的 Visual Studio 2010 工具：

- 安装 Visual Studio 时。

- 安装 Microsoft Office 时。

- 安装适用于 Office 运行时可再发行组件的 Visual Studio 2010 工具时。

  安装的运行时组件取决于计算机的配置和安装方案。

## <a name="runtime-components-that-are-installed-in-each-installation-scenario"></a>安装在每个安装方案中的运行时组件

 用于 Office 运行时的 Visual Studio 2010 工具具有三个组件： Office 解决方案加载程序、.NET Framework 3.5 的 Office 扩展以及 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本的 Office 扩展。 在安装运行时时，始终安装 Office 解决方案加载程序。 .NET Framework 的 Office 扩展的安装取决于计算机的配置和安装方案。 如果在首次安装运行时时 Office 扩展之一不能安装，则当满足某些需求时，运行时将稍后自动安装缺少的 Office 扩展。 运行时的此功能称为 *按需安装*。

 下表显示每个运行时安装方案中默认安装的运行时组件。 有关每个方案的详细信息将在后面显示。

|运行时安装方案|Office 解决方案加载程序|.NET Framework 3.5 的 Office 扩展|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 的 Office 扩展|[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 的 Office 扩展|
|-----------------------------------|----------------------------|--------------------------------------------------| - |---------------------------------------------------------------------------|
|通过 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 及更高版本|是|是的，如果已安装 .NET Framework 3.5。|是|是|
|有 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|是|是的，如果已安装 .NET Framework 3.5。|否|否|
|通过 Office 2010 Service Pack 1 (SP1) 或更高版本|是|是的，如果已安装 .NET Framework 3.5。|是的，如果已安装 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。|否|
|Office 2013 及更高版本|是|是的，如果已安装 .NET Framework 3.5|是的，如果已安装 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。|是的，如果已安装 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]。|
|通过运行时可再发行组件|是|是的，如果已安装 .NET Framework 3.5|是的，如果已安装 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]。|是的，如果已安装 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]。|

### <a name="install-the-runtime-with-visual-studio-or-the-microsoft-office-developer-tools-for-visual-studio"></a>安装运行时，将 Visual Studio 或 Microsoft Office 开发人员工具用于 Visual Studio

 在 Visual Studio 中安装 Office 开发人员工具时，[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 和 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 的 Office 扩展始终安装在开发计算机上。 仅当 .NET Framework 3.5 已位于开发计算机上时，才会安装 .NET Framework 3.5 的 Office 扩展。 如果在安装 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 后安装 .NET Framework 3.5，则在首次创建面向 .NET Framework 3.5 的 Office 项目时，运行时将自动安装 .NET Framework 3.5 的 Office 扩展。

> [!WARNING]
> 不能使用 [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] 或更高版本创建面向 .NET Framework 3.5 的 Office 项目。

 有关如何安装 Office 开发人员工具的详细信息，请参阅[如何：将计算机配置为开发 Office 解决方案](../vsto/how-to-configure-a-computer-to-develop-office-solutions.md)。

### <a name="install-the-runtime-with-office"></a>用 Office 安装运行时

 安装 Office 时，如果 .NET Framework 3.5 已位于计算机上，则安装 .NET Framework 3.5 的 Office 扩展。 如果在安装 Office 之后安装 .NET Framework 3.5，则在 Office 应用程序首次尝试加载面向 .NET Framework 3.5 的解决方案时，运行时将自动安装 .NET Framework 3.5 的 Office 扩展。

 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]如果计算机上已存在 .NET Framework 的相应版本，则或更高版本的 Office 扩展也会随 Office 一起安装。

 若要确保你的用户具有使用应用程序所需的扩展，请包括最新版本的 Visual Studio 2010 工具，用于 Office 运行时可再发行组件作为你的解决方案的先决条件。 有关先决条件的详细信息，请参阅[部署的 Office 解决方案先决条件](/previous-versions/bb608617(v=vs.110))。

### <a name="install-the-runtime-by-using-the-runtime-redistributable"></a>使用运行时可再发行组件安装运行时

 你可以通过手动运行运行时可再发行组件的 Visual Studio 2010 Office 工具来安装运行时，或在部署 Office 解决方案时包含可再发行组件作为必备组件。

 使用 Visual Studio 2010 Office 运行时可再发行组件安装运行时时， [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 如果计算机上已存在 Office 的相应版本，则会安装 .NET Framework 3.5 和或更高版本的 Office 扩展。 如果在运行时已安装的情况下计算机缺少 .NET Framework 的这些版本之一，则此时将不安装缺少的 .NET framework 版本的 Office 扩展。 如果你于稍后安装 .NET Framework 所缺少的版本，则下一次解决方案需要已安装（如果运行时与使用 ClickOnce 部署的解决方案一起安装）或已加载（如果运行时与使用 Windows Installer 部署的解决方案一起安装）扩展时，运行时将自动安装相应的 Office 扩展。

 有关在 ClickOnce 解决方案中包括先决条件的详细信息，请参阅[如何：在最终用户计算机上安装必备组件以运行 Office 解决方案](/previous-versions/bb608608(v=vs.110))。 有关如何手动安装可再发行组件包的运行时的详细信息，请参阅[如何：安装 Visual Studio Tools for Office 运行时可再发行组件](../vsto/how-to-install-the-visual-studio-tools-for-office-runtime-redistributable.md)。

## <a name="see-also"></a>请参阅

- [Visual Studio Tools for Office 运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [Visual Studio Tools for Office 运行时中的程序集](../vsto/assemblies-in-the-visual-studio-tools-for-office-runtime.md)
