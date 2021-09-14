---
title: 部署 & 将 SharePoint 解决方案发布到本地 SharePoint 站点
titleSuffix: ''
description: 查看如何将 SharePoint 解决方案部署或发布到开发计算机上的本地 SharePoint 服务器。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: 0ca33017e48db24a4f1ab055289683737d047c4e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663830"
---
# <a name="how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site"></a>如何：将 SharePoint 解决方案部署并发布到本地 SharePoint 网站
  你可以在开发计算机上将 SharePoint 解决方案部署或发布到本地 SharePoint 服务器。 部署过程会将 *.wsp* 文件复制到 SharePoint 服务器，安装解决方案，然后激活这些功能。 发布过程仅将 *.wsp* 文件复制到 SharePoint 服务器并安装该文件。 必须手动激活它，才能在 SharePoint 中启用它。

## <a name="to-deploy-a-sharepoint-solution-to-the-local-sharepoint-server"></a>将 SharePoint 解决方案部署到本地 SharePoint 服务器

1. 在 **解决方案资源管理器** 中，选择要部署的项目。

2. 在菜单栏上，依次选择 " **生成**"、" **部署解决方案**"。

     将在本地 SharePoint 服务器上创建并安装 *.wsp* 文件。 此外，还会激活这些功能。

## <a name="to-publish-a-sharepoint-solution-to-a-local-sharepoint-server"></a>将 SharePoint 解决方案发布到本地 SharePoint 服务器

1. 在 **解决方案资源管理器** 中，打开要发布的 SharePoint 项目的快捷菜单，然后选择 "**发布**"。

2. 在 " **发布** " 对话框中，选择 " **发布到文件系统** " 选项按钮。

3. 在 " **目标位置** " 文本框中，输入本地路径，然后选择 " **发布** " 按钮。

     发布进度会显示在 "Visual Studio **输出**" 窗口中。 完成此过程后，会在本地 SharePoint 服务器上安装解决方案 (*.wsp*) 文件。 但是，还必须将其激活，才能在 SharePoint 中使用。 如果解决方案文件已存在，则会出现错误，并询问您是否要覆盖现有文件。 有关升级包的信息，请参阅[如何：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)中有关升级远程包的部分。

## <a name="see-also"></a>另请参阅
- [如何：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：使用包设计器在包中添加和移除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
