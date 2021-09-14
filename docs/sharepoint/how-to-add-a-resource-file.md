---
title: 如何：添加资源文件|Microsoft Docs
description: 使用解决方案节点的快捷菜单Visual Studio中的功能节点，将资源文件添加到 解决方案资源管理器。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- resource files [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, resource files
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: b11fdbdda72f1929afc1f5d2726332246b312d07
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600621"
---
# <a name="how-to-add-a-resource-file"></a>如何：添加资源文件
  用于添加资源文件的命令位于解决方案节点的快捷菜单上，而功能节点位于解决方案资源管理器。 有关详细信息，请参阅本地化[SharePoint解决方案](../sharepoint/localizing-sharepoint-solutions.md)。

### <a name="to-add-a-global-resource-file-to-a-sharepoint-solution"></a>将全局资源文件添加到 SharePoint 解决方案

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，打开SharePoint解决方案。

2. 在 **解决方案资源管理器** 中，SharePoint项目节点，然后在菜单栏上选择  >  **"Project"添加新项"。**

3. 在" **添加新项"** 对话框中，选择" **全局资源文件** "模板，然后选择"添加 **"** 按钮。

   > [!NOTE]
   > "全局资源文件"项目项模板仅在SharePoint项目项时显示。

4. 在" **添加资源** "对话框中，选择资源文件的区域性，例如英语 (美国) 。

    此步骤将全局资源文件添加到解决方案，格式为 **Resource_x_。**<em>区域性</em><strong>。</strong>resx，例如 *Resource1.en-US.resx*。

5. 当资源 **编辑器在** 中打开 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 时，将资源添加到资源文件。

### <a name="to-add-a-feature-resource-file-to-a-sharepoint-feature"></a>将功能资源文件添加到SharePoint功能

1. 如果SharePoint解决方案尚未在 中打开 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，请打开解决方案。

2. 在 **解决方案资源管理器** 中，打开"功能"节点下功能名称的快捷菜单，然后选择"**添加功能资源"。**

     此步骤将资源文件添加到 _ResourceFileName 格式的功能_**。**_culture_**.resx**，例如 *Feature1.en-US.resx*。

3. 当资源 **编辑器在** 中打开 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 时，将资源添加到资源文件。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
