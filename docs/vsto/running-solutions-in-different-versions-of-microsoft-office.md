---
title: 在 Microsoft Office 的不同版本中运行解决方案
description: 了解如何运行使用 Visual Studio 2010 及更高版本创建的 Microsoft Office 解决方案版本。
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
# <a name="run-solutions-in-different-versions-of-microsoft-office"></a>在 Microsoft Office 的不同版本中运行解决方案

## <a name="run-office-solutions-created-by-using-visual-studio-2010-and-above"></a>运行 Office 使用 Visual Studio 2010 及更高版本创建的解决方案

|项目模板面向的 Office 版本|项目的目标 .NET Framework<sup>1</sup>|可以运行解决方案的 Office 版本|最终用户计算机上所需的运行时|
|--------------------------------------------------------|------------------------------------------------------|--------------------------------------------------|-------------------------------------------|
|Office 2016 和 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office 系统<sup>2</sup>|Visual Studio 2010 Tools for Office 运行时|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office 系统<sup>2</sup>|Visual Studio 2010 Tools for Office 运行时|
|[!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|.NET Framework 3.5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]|Visual Studio 2010 Tools for Office 运行时|
|2007 Microsoft Office system|[!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或更高版本，<br /><br /> 或<br /><br /> .NET Framework 3.5|Office 2016<br /><br /> [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]<br /><br /> [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<br /><br /> 2007 Microsoft Office system|Visual Studio 2010 Tools for Office 运行时|

 1. 要运行解决方案的最终用户计算机上需要项目目标 .NET Framework 版本。 例如，如果项目面向 .NET Framework 3.5，则最终用户计算机上需要 .NET Framework 3.5。 在此示例中，如果 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 最终用户计算机上仅安装了，则解决方案将不会运行。

 2. 在此情景中，只有当解决方案不使用 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 中的新功能时，它才会在 2007 Microsoft Office System 中正常运行。

## <a name="run-office-solutions-created-by-using-versions-of-visual-studio-prior-to-visual-studio-2010"></a>运行 Office 在 Visual Studio 2010 之前使用 Visual Studio 版本创建的解决方案
 可以运行使用 Visual Studio 2010 之前的 Visual Studio 版本创建的解决方案的 Microsoft Office 应用程序。 在某些情况下，这些解决方案要求使用 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的不同版本。 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]可以在同一台计算机上并行安装的不同版本。

 下表显示了哪些版本的 Microsoft Office 可以运行使用 Visual Studio 早期版本创建的解决方案，以及 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 每个解决方案所需的和 .NET Framework 的版本。

|用于创建解决方案的 Visual Studio 版本|项目模板面向的 Office 版本|可以运行解决方案的 Office 版本|最终用户计算机上所需的运行时|最终用户计算机上所需的 .NET Framework 版本|
|----------------------------------------------------------|--------------------------------------------------------|--------------------------------------------------|-------------------------------------------|----------------------------------------------------------|
|Visual Studio 2008 专业版<br /><br /> 或<br /><br /> Visual Studio Team System 2008|2007 Microsoft Office system|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)]<sup>1</sup><br /><br /> 2007 Microsoft Office system|用于 Office 运行时的 Visual Studio 2010 工具<sup>1</sup><br /><br /> 或<br /><br /> Visual Studio Tools for the Microsoft Office System（3.0 版 Runtime）|.NET Framework 3.5|
|安装了 VSTO 2005 标准版<sup>2</sup>的以下版本的 Visual Studio 2005：<br /><br /> -Visual Studio 2005 Office 工具<br />-Visual Studio 团队系统2005<br />-Visual Studio 2005 Professional|2007 Microsoft Office system|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] (仅限32位<sup></sup>) <br /><br /> 2007 Microsoft Office system|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET framework 2.0、.NET Framework 3.0 或 .NET Framework 3.5|
|Visual Studio 以下版本中的任何版本：<br /><br /> -Visual Studio 2008 Professional<br />-Visual Studio 团队系统2008<br />-Visual Studio 2005 Office (的工具（有或不含 VSTO 2005 标准版<sup>2</sup> ）) <br />-Visual Studio 的 Team System 2005 (VSTO 2005 标准版<sup>2</sup>安装) <br />-Visual Studio 2005 Professional 安装 VSTO 2005 标准版<sup>2</sup>|Microsoft Office 2003|[!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] (仅限32位<sup></sup>) <br /><br /> 2007 Microsoft Office system<br /><br /> Microsoft Office 2003|Visual Studio 2005 Tools for Office Second Edition Runtime|.NET framework 2.0、.NET Framework 3.0 或 .NET Framework 3.5|

 1. [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)]和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 应用程序包括用于 Office 运行时的 Visual Studio 2010 工具。 因此，在这种情况下，这些应用程序始终使用适用于 Office 运行时的 Visual Studio 2010 工具，而不是 Microsoft Office 系统 (版本3.0 运行时) 的 Visual Studio Tools。 2007 Microsoft Office System 中的应用程序可以使用 Visual Studio 2010 Tools Office 运行时或 Visual Studio Tools for Microsoft Office System（3.0 版 Runtime）。

 2. VSTO 2005 SE 是免费的 Visual Studio 外接程序，它提供 Microsoft Office 2003 和 2007 Microsoft Office 系统的 VSTO 外接程序项目模板。 可以通过 Visual Studio 2005 专业版、Visual Studio 2005 Tools for Office 或 Visual Studio Team System 2005 的某一版本安装它。 有关详细信息，请参阅[Visual Studio 2005 Tools for Office Second Edition](https://developer.microsoft.com/office/docs)。

 3. 需要 Visual Studio 2005 Tools for Office Second Edition Runtime 的 Office 解决方案与 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 和 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 的 64 位版本不兼容。 若要在 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 或 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 的 64 位版本中运行这些解决方案，必须将项目升级为 [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] 或面向 2007 Microsoft Office System 的 Visual Studio 2008 项目。

## <a name="see-also"></a>另请参阅
- [设计和创建 Office 解决方案](../vsto/designing-and-creating-office-solutions.md)
- [Visual Studio Tools for Office 运行时概述](../vsto/visual-studio-tools-for-office-runtime-overview.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Visual Studio Tools for Office 运行时安装方案](../vsto/visual-studio-tools-for-office-runtime-installation-scenarios.md)
- [将计算机配置为开发 Office 解决方案](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)
