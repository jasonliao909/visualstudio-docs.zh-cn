---
title: 远程部署、发布&升级SharePoint解决方案
titleSuffix: ''
description: 在远程站点或本地 SharePoint站点上部署、发布和升级沙盒SharePoint解决方案。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- remote deployment [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, remote deployment
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: sharepoint-development
ms.workload:
- office
ms.openlocfilehash: fb4838625029a95f2c7b6d55cfba22284c168818
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663829"
---
# <a name="how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server"></a>如何：部署、发布和升级SharePoint远程服务器上部署、发布和升级解决方案
  除了将SharePoint部署到本地系统之外，还可以将沙盒SharePoint解决方案发布到远程站点或本地SharePoint站点。 远程发布过程将 *.wsp* 文件复制到 SharePoint 服务器，安装解决方案，然后使你能够激活解决方案。 还可以在远程SharePoint解决方案安装后升级远程部署解决方案安装。

## <a name="to-publish-a-sandboxed-sharepoint-solution-to-a-remote-sharepoint-server"></a>将沙盒SharePoint解决方案发布到远程SharePoint服务器

1. 在 **解决方案资源管理器** 中，打开要发布的沙盒SharePoint项目的快捷菜单，然后选择"发布 **"。**

2. 在"**发布"** 对话框中，选择"发布到 SharePoint **站点**"选项按钮，然后输入联机发布站点的 URL，例如 `https://mytestsite.sharepoint.microsoftonline.com` ：。

3. 选择" **发布后在浏览器中打开** 解决方案库"页选项按钮，在发布后在"解决方案库"页 **中** 查看解决方案列表。

4. 选择 **“发布”** 按钮。

5. 如果需要用户身份验证，请登录到远程服务器。

     发布进度将显示在"输出Visual Studio **窗口中**。 完成此过程后，解决方案 (*.wsp*) 安装在远程SharePoint服务器上。 但是，必须先激活它，然后才能在 SharePoint。

6. 在"**解决方案库"** 页上，选择SharePoint应用程序，然后在功能区上选择"激活 **"** 按钮。

7. 在" **激活解决方案"** 对话框的功能区上，再次选择" **激活"** 按钮。

     " **解决方案** 库"页上 **的"状态** "列指示应用程序处于活动状态。

## <a name="to-upgrade-a-sandboxed-sharepoint-solution-on-a-remote-sharepoint-server"></a>升级远程 SharePoint 服务器上沙盒SharePoint解决方案
 如果沙盒SharePoint解决方案已在远程服务器上发布，则通过以下过程可以在 中更改应用程序后升级 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 它。

1. 在 中SharePoint包 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 为此， **请解决方案资源管理器打开** 包。 它显示在包 **资源管理器 中**。

2. 在 **"包资源管理器**"的" **名称"** 框中，将包名称更改为唯一名称。

3. 保存项目。

4. 在 **解决方案资源管理器** 中，打开项目的快捷菜单，然后选择"发布 **"。**

5. 在"**发布"** 对话框中，选择"发布到 SharePoint 站点"选项按钮，然后，如果缺少保存解决方案的远程服务器的 URL，请输入它。

6. 选择" **发布后在浏览器中打开** 解决方案库"页选项按钮，在发布后在"解决方案库"页 **中** 查看解决方案列表。

7. 选择 **“发布”** 按钮。

8. 如果需要用户身份验证，请登录到远程服务器。

     如果最近登录到远程服务器，可能不需要身份验证。

     如果 SharePoint 服务器上仍然存在同名应用程序的旧版本，则你收到一个错误，指出同名的包已在 SharePoint 服务器上。 发布前，必须将包重命名为唯一名称。

9. 在"SharePoint"中选择新应用程序，然后在功能区上选择"升级 **"** 按钮。

10. 在" **升级解决方案"** 对话框的功能区上，再次选择" **升级"** 按钮。 " **解决方案** 库"页上 **的"状态** "列现在应指示应用程序处于活动状态。

     停用解决方案的旧版本，使用旧解决方案中维护的数据升级解决方案的新版本，在SharePoint。

## <a name="see-also"></a>另请参阅
- [如何：将 SharePoint 解决方案部署到本地 SharePoint 站点](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)
- [创建SharePoint解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义SharePoint包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：使用包设计器向包添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
