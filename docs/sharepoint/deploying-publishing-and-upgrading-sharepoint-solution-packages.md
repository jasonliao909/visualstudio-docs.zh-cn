---
title: 部署、发布&升级SharePoint解决方案包
description: 部署、发布和升级SharePoint解决方案包。 自定义部署过程。 将包发布到远程或本地服务器。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SharePointProjectPropertyTab
- VS.SharePointTools.Project.Publishing
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
ms.openlocfilehash: d0dd6332a6ce1f7b0a1940e392918004f246cc525ab48030c15085b82ba54d42
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121425526"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>部署、发布和升级SharePoint解决方案包
  在 Visual Studio 中开发 SharePoint 解决方案后，可以将其包 (.wsp) 文件部署到本地 SharePoint 服务器，或将其发布到远程或本地 SharePoint 服务器。 如果部署文件，可以自定义包文件 (.wsp) 部署。

> [!NOTE]
> 目前，只能将沙盒解决方案发布到远程SharePoint服务器。 有关详细信息，请参阅 [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

## <a name="deploy-publish-and-upgrade"></a>部署、发布和升级
 *部署* 是指将SharePoint中从本地SharePoint生成Visual Studio文件复制到本地主机。 在已部署的解决方案中，可以配置部署步骤，例如Internet Information Services (IIS) 池、在部署后激活解决方案等。 若要部署，请使用"生成 **"** 菜单上的" **部署"** 命令。 有关详细信息，请参阅[如何：](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)编辑 SharePoint 部署配置和[如何：](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)将 SharePoint 解决方案部署到本地 SharePoint 站点。

 *发布* 是指将沙盒SharePoint解决方案文件上传到远程SharePoint站点;即位于另一个系统上的站点。 还可以将SharePoint沙盒解决方案文件发布到本地 SharePoint 站点，但无论发布到 的站点是本地站点还是远程站点，都无法配置其部署步骤。

 *升级* 是指更新远程或本地发布的现有SharePoint解决方案。 对 Visual Studio 中的 SharePoint 解决方案进行了任何更改后，请更改解决方案的包文件名，重新发布解决方案，然后在解决方案成功重新发布后升级该解决方案。 如果重新发布本地发布的解决方案，可以覆盖现有解决方案文件。

## <a name="deploy-packages"></a>部署包
 可以将包文件部署到开发SharePoint服务器上进行测试和调试。 还可以创建一个包文件，可通过选择"发布"对话框中的"发布到文件系统"选项按钮，在另一台计算机 **中** 安装该文件。 创建包并复制到指定的本地文件路径。 若要将SharePoint解决方案部署到本地服务器，请使用"生成"菜单上的"部署 **"** 命令。 有关详细信息，请参阅[如何：将](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)SharePoint 解决方案部署到本地 SharePoint 站点。

 若要了解如何部署列表定义、添加事件接收器以及使用功能设计器和包设计器，请参阅 [演练：部署项目任务列表定义](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md)。

## <a name="customize-the-deployment-process"></a>自定义部署过程
 下表显示了调试和部署解决方案时可以使用的两SharePoint配置。

|部署配置|说明|
|------------------------------|-----------------|
|默认|默认部署配置。 执行以下部署步骤：<br /><br /> 1.运行预部署命令。<br />2.回收 IIS 应用程序池。<br />3.收回解决方案。<br />4.添加解决方案。<br />5.激活功能。<br />6.运行部署后命令。<br /><br /> 卸载包时，将执行以下收回步骤。<br /><br /> 1.回收 IIS 应用程序池。<br />2.收回解决方案。|
|无激活|此部署配置运行的步骤与默认配置相同，但会跳过激活步骤。|

 可以创建自己的部署配置以完成单个步骤，或更改部署过程中的步骤顺序。 有关详细信息，请参阅[如何：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)。

 还可以添加在部署之前和之后运行的命令。 有关详细信息，请参阅[如何：设置SharePoint命令](../sharepoint/how-to-set-sharepoint-deployment-commands.md)。

## <a name="publish-packages-to-a-remote-or-local-server"></a>将包发布到远程或本地服务器
 若要将沙盒 SharePoint 解决方案发布到远程服务器，请选择菜单栏上的"生成"和"发布"，然后在"发布"对话框中，选择"发布到 SharePoint **站点"** 选项按钮，并提供远程服务器的 URL，例如 `https://someremoteserver.sharepoint.microsoftonline.com` 。

 若要将SharePoint发布到本地服务器，在"发布"对话框中，选择"发布到文件系统"选项按钮，并提供本地系统路径。

 成功将解决方案发布到 SharePoint，解决方案会显示在解决方案 **库中，** 可在其中激活它。 有关详细信息，请参阅如何：在远程服务器上部署、SharePoint[和升级解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

### <a name="upgrade-published-packages"></a>升级已发布的包
 如果在发布发布后对 SharePoint项目Visual Studio更改，则必须升级已发布的包以包括更改。 若要成功升级，包必须具有唯一的名称。 如果在 SharePoint 站点上找到同名的包（在更新现有应用程序时可能会发生此情况）时，错误会提醒你文件名冲突，并允许您重命名包。 重新发布后，新包会显示在 SharePoint站点上，并且可以升级。 升级后的包使用旧包的数据更新解决方案，然后在 SharePoint。 有关详细信息，请参阅如何：在远程服务器上部署、SharePoint[和升级解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
