---
title: 操作说明：添加资源文件 | Microsoft Docs
description: 在 Visual Studio 中，使用“解决方案资源管理器”中解决方案节点和功能节点的快捷菜单上的命令添加资源文件。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600621"
---
# <a name="how-to-add-a-resource-file"></a>如何：添加资源文件
  用于添加资源文件的命令位于“解决方案资源管理器”中解决方案节点和功能节点的快捷菜单上。 有关详细信息，请参阅[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)。

### <a name="to-add-a-global-resource-file-to-a-sharepoint-solution"></a>将全局资源文件添加到 SharePoint 解决方案

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中，打开 SharePoint 解决方案。

2. 在“解决方案资源管理器”中选择 SharePoint 项目节点，然后在菜单栏上依次选择“项目” > “添加新项”。

3. 在“添加新项”对话框中，选择“全局资源文件”模板，然后选择“添加”按钮。

   > [!NOTE]
   > “全局资源文件”项目项模板仅在选择 SharePoint 项目项时显示。

4. 在“添加资源”对话框中，选择资源文件的区域性，例如英语(美国)。

    此步骤将全局资源文件添加到解决方案，格式为 Resource_x_.<em>culture</em>.resx，例如 Resource1.en-US.resx。

5. 当“资源编辑器”在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中打开时，将资源添加到资源文件。

### <a name="to-add-a-feature-resource-file-to-a-sharepoint-feature"></a>将功能资源文件添加到 SharePoint 功能

1. 如果 SharePoint 解决方案尚未在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中打开，请打开解决方案。

2. 在“解决方案资源管理器”中，打开“功能”节点下功能名称的快捷菜单，然后选择“添加功能资源”。

     此步骤将资源文件添加到功能，格式为 ResourceFileName.culture **.resx**，例如，Feature1.en-US.resx。

3. 当“资源编辑器”在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中打开时，将资源添加到资源文件。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
