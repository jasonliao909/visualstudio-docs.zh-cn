---
title: 在不同版本的服务中运行Microsoft Office
description: 了解如何运行使用 Microsoft Office 2010 及Visual Studio创建的解决方案的版本。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- solutions [Office development in Visual Studio], multiple Office versions
- Office applications [Office development in Visual Studio], multiple Office versions
- Office development in Visual Studio, multiple Office versions
- Office solutions [Office development in Visual Studio]
- multiple Office versions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 65d3338307668ce07b2a08aa7bc2f97ab3b09fbd1280767e06ad897194a58272
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121408162"
---
# <a name="run-solutions-in-different-versions-of-microsoft-office"></a>在不同版本的服务中运行Microsoft Office

## <a name="run-office-solutions-created-by-using-visual-studio-2010-and-above"></a>运行Office 2010 及Visual Studio创建的解决方案

|项目模板面向的 Office 版本|项目.NET Framework<sup>1</sup>的目标目标|可以运行解决方案的 Office 版本|最终用户计算机上所需的运行时|
|--------------------------------------------------------|------------------------------------------------------|--------------------------------------------------|-------------------------------------------|
|Office 2016 和 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office系统<sup>2</sup>|Visual Studio 2010 Tools for Office 运行时|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office系统<sup>2</sup>|Visual Studio 2010 Tools for Office 运行时|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|.NET Framework 3.5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|Visual Studio 2010 Tools for Office 运行时|
|2007 Microsoft Office system|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，<br /><br /> 或<br /><br /> .NET Framework 3.5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office system|Visual Studio 2010 Tools for Office 运行时|

 1. 在.NET Framework计算机上运行解决方案所需的项目目标版本。 例如，如果项目面向 .NET Framework 3.5，.NET Framework最终用户计算机上需要 3.5。 此示例中，如果仅在最终用户计算机上安装 ，则 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 解决方案将不会运行。

 2. 在此情景中，只有当解决方案不使用 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 中的新功能时，它才会在 2007 Microsoft Office System 中正常运行。

## <a name="run-office-solutions-created-by-using-versions-of-visual-studio-prior-to-visual-studio-2010"></a>运行Office 2010 之前的 Visual Studio 版本创建Visual Studio解决方案
 可以运行使用 Visual Studio 2010 之前的 Visual Studio 版本创建的解决方案的 Microsoft Office 应用程序。 在某些情况下，这些解决方案要求使用 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的不同版本。 的不同版本的 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 可以并排安装在同一计算机上。

 下表显示哪些版本的 Microsoft Office 可以运行使用以前版本的 Visual Studio 创建的解决方案，以及每个解决方案需要哪些版本的 .NET Framework 和 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] .NET Framework。

|用于创建解决方案的 Visual Studio 版本|项目模板面向的 Office 版本|可以运行解决方案的 Office 版本|最终用户计算机上所需的运行时|最终用户.NET Framework所需的版本|
|----------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------|-------------------------------------------|----------------------------------------------------------|
|Visual Studio 2008 专业版<br /><br /> 或<br /><br /> Visual Studio Team System 2008|2007 Microsoft Office system|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<sup>1</sup><br /><br /> 2007 Microsoft Office system|Visual Studio 2010 Tools for Office Runtime<sup>1</sup><br /><br /> 或<br /><br /> Visual Studio Tools for the Microsoft Office System（3.0 版 Runtime）|.NET Framework 3.5|
|安装了 2005 Visual Studio 2005 VSTO 2 的 标准版<sup>版本</sup>之一：<br /><br /> - Visual Studio 2005 Tools for Office<br />- Visual Studio Team System 2005<br />- Visual Studio 2005 Professional|2007 Microsoft Office system|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] (32 位<sup>，仅 3</sup>) <br /><br /> 2007 Microsoft Office system|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET framework 2.0、.NET Framework 3.0 或 .NET Framework 3.5|
|Visual Studio 以下版本中的任何版本：<br /><br /> - Visual Studio 2008 Professional<br />- Visual Studio Team System 2008<br />- Visual Studio 2005 工具Office (安装有 2005 VSTO，标准版<sup>2</sup>) <br />- Visual Studio Team System 2005 (或不带 VSTO 2005 标准版<sup>2</sup>) <br />- Visual Studio 2005 Professional 2005 VSTO 2 标准版<sup>2</sup>|Microsoft Office 2003|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] (32 位<sup>，仅 3</sup>) <br /><br /> 2007 Microsoft Office system<br /><br /> Microsoft Office 2003|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET framework 2.0、.NET Framework 3.0 或 .NET Framework 3.5|

 1. [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]和应用程序 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 包括 Visual Studio 2010 Tools for Office 运行时。 因此，在此方案中，这些应用程序始终使用 Visual Studio 2010 Tools for Office 运行时，而不是 Visual Studio Tools Microsoft Office 系统 (版本 3.0 Runtime) 。 2007 Microsoft Office System 中的应用程序可以使用 Visual Studio 2010 Tools Office 运行时或 Visual Studio Tools for Microsoft Office System（3.0 版 Runtime）。

 2. VSTO 2005 SE 是免费的 Visual Studio 外接程序，它提供 Microsoft Office 2003 和 2007 Microsoft Office 系统的 VSTO 外接程序项目模板。 可以通过 Visual Studio 2005 专业版、Visual Studio 2005 Tools for Office 或 Visual Studio Team System 2005 的某一版本安装它。 有关详细信息，请参阅[Visual Studio 2005 Tools for Office Second Edition](https://developer.microsoft.com/office/docs)。

 3. 需要 Visual Studio 2005 Tools for Office Second Edition Runtime 的 Office 解决方案与 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 的 64 位版本不兼容。 若要在 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 或 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 的 64 位版本中运行这些解决方案，必须将项目升级为 [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] 或面向 2007 Microsoft Office System 的 Visual Studio 2008 项目。

## <a name="see-also"></a>请参阅
- [设计和创建Office解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Visual Studio Tools for Office运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Visual Studio Tools for Office运行时安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)
- [配置计算机以开发Office解决方案](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)
