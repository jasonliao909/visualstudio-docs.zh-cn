---
title: 如何：编辑SharePoint部署配置|Microsoft Docs
description: 了解如何创建部署SharePoint或修改现有部署配置。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.Project.DeploymentConfig
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 295c756457cbc8326bcd80d3b92c2ad233d2cb7a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126666183"
---
# <a name="how-to-edit-a-sharepoint-deployment-configuration"></a>如何：编辑SharePoint部署配置
  可以创建部署配置或修改现有部署配置。 例如，可以运行单个步骤或更改部署过程中的步骤顺序。 你可能想要创建或修改部署配置，因为无法更改内置配置和以编程方式添加的配置。

## <a name="create-a-sharepoint-deployment-configuration"></a>创建SharePoint部署配置

#### <a name="to-create-a-sharepoint-deployment-configuration"></a>创建SharePoint部署配置

1. 在 **解决方案资源管理器** 中，选择SharePoint项目，然后在菜单栏上，选择 **"Project"**_项目名称_**属性"。**

2. 在 **"SharePoint"** 选项卡上，选择"新建 **"** 按钮。

     将出现 **"添加新部署配置** "对话框。

3. 在 **"名称** "文本框中，输入部署配置的名称。

4. 在" **可用部署步骤** "窗格中，选择要添加到部署配置的步骤，选择" () "按钮，然后选择" **>** 确定 **"** 按钮。

    > [!NOTE]
    > 如果已配置部署前命令或部署后命令，则只有在将它们添加到自定义部署配置时，这些步骤才运行。

## <a name="change-the-active-deployment-configuration"></a>更改活动部署配置

#### <a name="to-change-the-active-deployment-configuration"></a>更改活动部署配置

1. 在 **解决方案资源管理器** 中，选择SharePoint项目，然后在菜单栏上选择"Project  >  **\<*ProjectName*> 属性"。**

2. 选择 **"SharePoint** 选项卡。

3. 在 **"活动部署配置** "列表框中，选择想要使用的部署配置的名称。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
