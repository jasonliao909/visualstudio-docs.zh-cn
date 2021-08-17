---
title: 沙盒解决方案和场解决方案之间的差异|Microsoft Docs
description: 了解沙盒和场解决方案之间的差异。 了解如何Visual Studio使用任一类型的解决方案进行调试。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, sandboxed solutions
- sandboxed solutions [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, farm solutions
- farm solutions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: f05341a4914d3864d2e57a223272eb8b326785a6d6cf9ca4703e6e585b228804
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121332347"
---
# <a name="differences-between-sandboxed-and-farm-solutions"></a>沙盒解决方案和场解决方案之间的差异
  编译一个SharePoint解决方案时，它会部署到 SharePoint 服务器，并附加到调试器以对其进行调试。 用于调试解决方案的过程取决于沙盒解决方案属性的设置：沙盒解决方案或场解决方案。

 有关详细信息，请参阅 [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

## <a name="farm-solutions"></a>场解决方案
 托管在 IIS 工作进程 (W3WP.exe) 的场解决方案运行可能影响整个场的代码。 调试其"沙盒解决方案"属性设置为"场解决方案"的 SharePoint 项目时，系统的 IIS 应用程序池在 SharePoint 收回或部署该功能之前回收，以便释放由 IIS 工作进程锁定的任何文件。 仅回收为项目站点 URL SharePoint IIS 应用程序池。

## <a name="sandboxed-solutions"></a>沙盒解决方案
 沙盒解决方案托管在 SharePoint 用户代码解决方案工作进程 (SPUCWorkerProcess.exe) 运行仅影响解决方案网站集的代码。 由于沙盒解决方案不在 IIS 工作进程中运行，因此 IIS 应用程序池和 IIS 服务器都不得重启。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将调试器附加到 SPUSerCodeV4 服务自动触发SharePoint SPUCWorkerProcess 进程。 SPUCWorkerProcess 进程不需要回收来加载最新版本的解决方案。

## <a name="either-type-of-solution"></a>任一类型的解决方案
 对于任一解决方案类型， [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 也会将调试器附加到浏览器以启用客户端脚本调试。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用脚本调试引擎实现此目的。 若要启用脚本调试，必须在系统提示时更改默认浏览器设置。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 仅将调试器附加到运行当前站点的 W3WP 或 SPUCWorkerProcess 进程。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 还附加托管 COM Plus 和工作流调试引擎。

## <a name="see-also"></a>请参阅
- [调试SharePoint解决方案](../sharepoint/debugging-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)
