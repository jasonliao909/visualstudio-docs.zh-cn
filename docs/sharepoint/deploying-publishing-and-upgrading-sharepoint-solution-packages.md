---
title: 部署、发布和升级 SharePoint 解决方案包
description: 部署、发布和升级 SharePoint 解决方案包。 自定义部署过程。 将包发布到远程服务器或本地服务器。
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
ms.openlocfilehash: 3101e0f546026f9d030b87238ce7d1630b4ab581
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601014"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>部署、发布和升级 SharePoint 解决方案包
  在 Visual Studio 中开发 SharePoint 解决方案后，可以将其包 (.wsp) 文件部署到本地 SharePoint 服务器，或者将其发布到远程或本地 SharePoint 服务器。 如果部署这些文件，你可以自定义包文件 (.wsp) 的部署方式。

> [!NOTE]
> 目前，只能将沙盒解决方案发布到远程 SharePoint 服务器。 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

## <a name="deploy-publish-and-upgrade"></a>部署、发布和升级
 部署是指将从 Visual Studio 中 SharePoint 项目生成的 SharePoint 解决方案文件复制到本地主机。 在已部署的解决方案中，你可以配置部署步骤，如回收 Internet Information Services (IIS) 池、部署后激活解决方案等。 若要部署，请使用“生成”菜单上的“部署”命令 。 有关详细信息，请参阅[操作说明：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)和[操作说明：将 SharePoint 解决方案部署和发布到本地 SharePoint 网站](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)。

 发布是指将沙盒 SharePoint 解决方案文件上传到远程 SharePoint 网站；即，位于另一个系统上的网站。 还可将 SharePoint 沙盒解决方案文件发布到本地 SharePoint 网站，但无论是发布到本地还是远程网站，你都不能配置其部署步骤。

 升级指的是更新现有的远程或本地发布的 SharePoint 解决方案。 在 Visual Studio 中对 SharePoint 解决方案进行任何更改后，都需要更改解决方案包文件名，重新发布解决方案，然后在成功重新发布后升级解决方案。 如果重新发布本地发布的解决方案，则可覆盖现有解决方案文件。

## <a name="deploy-packages"></a>部署包
 可将包文件部署到开发计算机上的 SharePoint 服务器以进行测试和调试。 还可选择“发布”对话框中的“发布到文件系统”选项按钮，创建可以安装在另一台计算机上的包文件 。 包将完成创建并被复制到指定的本地文件路径。 若要将 SharePoint 解决方案部署到本地服务器，请使用“生成”菜单上的“部署”命令 。 有关详细信息，请参阅[操作说明：将 SharePoint 解决方案部署和发布到本地 SharePoint 网站](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)。

 若要了解如何部署列表定义、添加事件接收器以及使用功能设计器和包设计器，请参阅[演练：部署项目任务列表定义](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md)。

## <a name="customize-the-deployment-process"></a>自定义部署过程
 下表显示了调试和部署 SharePoint 解决方案时可使用的两个部署配置。

|部署配置|说明|
|------------------------------|-----------------|
|默认|默认的部署配置。 执行以下部署步骤：<br /><br /> 1. 运行预先部署命令。<br />2. 回收 IIS 应用程序池。<br />3. 收回解决方案。<br />4. 添加解决方案。<br />5. 激活功能。<br />6. 运行后期部署命令。<br /><br /> 卸载包时，将执行以下收回步骤。<br /><br /> 1. 回收 IIS 应用程序池。<br />2. 收回解决方案。|
|无激活|此部署配置运行与默认配置相同的步骤，但会跳过激活步骤。|

 你可创建自己的部署配置来完成单个步骤或更改部署过程中的步骤顺序。 有关详细信息，请参阅[如何：编辑 SharePoint 部署配置](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md)。

 还可添加在部署前和部署后运行的命令。 有关详细信息，请参阅[操作说明：设置 SharePoint 部署命令](../sharepoint/how-to-set-sharepoint-deployment-commands.md)。

## <a name="publish-packages-to-a-remote-or-local-server"></a>将包发布到远程服务器或本地服务器
 若要将沙盒 SharePoint 解决方案发布到远程服务器，请在菜单栏上依次选择“生成”和“发布”，然后在“发布”对话框中，选择“发布到 SharePoint 网站”选项按钮，提供远程服务器的 URL，如 `https://someremoteserver.sharepoint.microsoftonline.com`   。

 若要将沙盒 SharePoint 解决方案发布到本地服务器，请在“发布”对话框中，选择“发布到文件系统”选项按钮，并提供本地系统路径 。

 解决方案成功发布到 SharePoint 后，它将显示在“解决方案库”中，你可以在此处激活它。 [操作说明：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

### <a name="upgrade-published-packages"></a>升级发布的包
 如果发布 Visual Studio 中的 SharePoint 项目后对其进行了任何更改，则必须升级已发布的包以包含这些更改。 若要成功升级，包必须具有唯一的名称。 如果在 SharePoint 网站上发现同名的包（在更新现有应用程序时可能会出现这种情况），则会出现一个错误，提醒你文件名冲突并让你重命名该包。 重新发布后，新的包将显示在 SharePoint 网站上并可进行升级。 升级的包使用较旧包中的数据更新解决方案，然后在 SharePoint 中激活解决方案。 [操作说明：在远程服务器上部署、发布和升级 SharePoint 解决方案](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md)。

## <a name="see-also"></a>另请参阅
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
