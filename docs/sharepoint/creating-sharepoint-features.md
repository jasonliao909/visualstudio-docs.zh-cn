---
title: 创建SharePoint功能|Microsoft Docs
description: 创建一SharePoint功能，以便对项目SharePoint相关项进行分组，以便更轻松地进行部署。 向解决方案SharePoint功能。 使用功能设计器。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
- features [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 4eaf4a9541834215c0c66aed7bb9271faa79a1e3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106843"
---
# <a name="create-sharepoint-features"></a>创建SharePoint功能
  可以使用"SharePoint功能"将相关的SharePoint项目项分组，以便更轻松地部署。 可以使用"功能设计器"创建功能、设置范围，以及将其他功能标记为SharePoint依赖项。 设计器还会生成清单，该清单是描述每个特征的 XML 文件。

## <a name="add-features-to-the-sharepoint-solution"></a>将功能添加到 SharePoint 解决方案
 可以使用"打包资源管理器"或SharePoint"将功能解决方案资源管理器解决方案。 可以使用以下方法之一添加功能。

- 在 **解决方案资源管理器** 中，打开"功能"的快捷 **菜单**，然后选择"**添加功能"。**

- 在 **"打包资源管理器**"中，打开包的快捷菜单，然后选择"**添加功能"。**

## <a name="using-the-feature-designer"></a>使用功能设计器
 一SharePoint解决方案可以包含一个或多个SharePoint功能，这些功能在解决方案中的"功能"节点下解决方案资源管理器。 每个功能都有自己的 **功能设计器** ，可用于自定义功能属性。 有关详细信息，请参阅[如何：自定义 SharePoint 功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)中的说明进行操作。 若要区分功能，可以配置功能属性，例如标题、说明、版本和范围。

### <a name="feature-designer-options"></a>功能设计器选项
 创建功能后，可以使用功能设计器对其进行自定义。

 下表描述了功能设计器中显示的功能属性。

|属性|说明|
|--------------|-----------------|
|标题|可选。 功能的默认标题设置为 *SolutionName* *FeatureName*。|
|说明|可选。 功能SharePoint说明。|
|范围|必需。 如果功能是通过使用 **解决方案资源管理器创建的，** 则默认情况下范围设置为 Web。<br /><br /> - 场：激活整个服务器场的功能。<br /><br /> - 站点：为网站集中的所有网站激活功能。<br /><br /> - Web：为特定网站激活功能。<br /><br /> - WebApplication：为 Web 应用程序中的所有网站激活功能。|
|解决方案中的项|可SharePoint功能的所有项目。|
|功能中的项|该SharePoint已添加到功能的项目项。|

## <a name="add-and-remove-sharepoint-project-items"></a>添加和SharePoint项目项
 可以选择要SharePoint要添加"部署功能"的SharePoint项目项。 使用 **功能设计器向** 功能添加和删除项，并查看功能清单。 有关详细信息，请参阅[如何：添加和删除项以SharePoint功能](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)。

## <a name="add-feature-dependencies"></a>添加功能依赖项
 可以配置功能清单，使 SharePoint 服务器在激活功能之前激活某些功能。 例如，如果SharePoint功能依赖于功能或数据的其他功能，SharePoint 服务器可以先尝试激活功能所依赖的任何功能。 有关详细信息，请参阅 [如何：添加和删除功能依赖项](../sharepoint/how-to-add-and-remove-feature-dependencies.md)。

## <a name="see-also"></a>请参阅
- [如何：自定义SharePoint功能](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [如何：添加和删除项以SharePoint功能](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
- [如何：添加和删除功能依赖项](../sharepoint/how-to-add-and-remove-feature-dependencies.md)
