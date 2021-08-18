---
title: 如何：添加资源文件 |Microsoft Docs
description: 使用解决方案资源管理器中解决方案节点和功能节点的快捷菜单上的命令，在 Visual Studio 中添加资源文件。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122149034"
---
# <a name="how-to-add-a-resource-file"></a>如何：添加资源文件
  用于添加资源文件的命令位于解决方案资源管理器中解决方案节点和功能节点的快捷菜单中。 有关详细信息，请参阅[本地化 SharePoint 解决方案](../sharepoint/localizing-sharepoint-solutions.md)。

### <a name="to-add-a-global-resource-file-to-a-sharepoint-solution"></a>将全局资源文件添加到 SharePoint 解决方案中

1. 在中 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，打开 SharePoint 解决方案。

2. 在 **解决方案资源管理器** 中，选择 "SharePoint 项目" 节点，然后在菜单栏上选择 " **Project**  >  **添加新项**"。

3. 在 " **添加新项** " 对话框中，选择 " **全局资源文件** " 模板，然后选择 " **添加** " 按钮。

   > [!NOTE]
   > 仅当选择 SharePoint 项目项时，才会显示 "全局资源文件" 项目项模板。

4. 在 " **添加资源** " 对话框中，选择资源文件的区域性，如 "英语 (美国) "。

    此步骤将全局资源文件添加到解决方案，格式为 Resource_x_ **。**<em>区域性</em><strong>。</strong>.resx，如， *resource1.resx*。

5. 当 **资源编辑器** 在中打开时 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，将资源添加到资源文件中。

### <a name="to-add-a-feature-resource-file-to-a-sharepoint-feature"></a>将功能资源文件添加到 SharePoint 功能

1. 如果未在中打开 SharePoint 解决方案 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，请打开解决方案。

2. 在 **解决方案资源管理器** 中，打开 " **功能** " 节点下某个功能的名称的快捷菜单，然后选择 " **添加功能资源**"。

     此步骤将资源文件添加到该功能，格式为 _ResourceFileName_**。**_区域性_**.resx**，如， *Feature1*）。

3. 当 **资源编辑器** 在中打开时 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ，将资源添加到资源文件中。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
