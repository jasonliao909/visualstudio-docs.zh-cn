---
title: 远程部署、发布和升级 SharePoint 解决方案
titleSuffix: ''
description: 在远程站点或本地 SharePoint 站点上部署、发布和升级沙盒 SharePoint 解决方案。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126663829"
---
# <a name="how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server"></a>如何：在远程服务器上部署、发布和升级 SharePoint 解决方案
  除了将 SharePoint 解决方案部署到本地系统，还可以将沙盒 SharePoint 解决方案发布到远程站点或本地 SharePoint 站点。 远程发布过程会将 .wsp 文件复制到 SharePoint 服务器，安装解决方案，然后可以激活这些解决方案。 还可以在对其进行更改之后升级远程 SharePoint 解决方案安装。

## <a name="to-publish-a-sandboxed-sharepoint-solution-to-a-remote-sharepoint-server"></a>若要将沙盒 SharePoint 解决方案发布到远程 SharePoint 服务器

1. 在“解决方案资源管理器”中，打开要发布的沙盒 SharePoint 项目的快捷菜单，然后选择“发布”。

2. 在“发布”对话框中，选择“发布到 SharePoint 站点”选项按钮，然后输入在线发布站点的 URL，例如：`https://mytestsite.sharepoint.microsoftonline.com`。

3. 选择“发布后在浏览器中打开解决方案库页”选项按钮，以便在发布后查看“解决方案库”页中的解决方案列表。 

4. 选择 **“发布”** 按钮。

5. 如果需要进行用户身份验证，请登录到远程服务器。

     发布进度显示在 Visual Studio“输出”窗口中。 完成此过程后，会在远程 SharePoint 服务器上安装解决方案 .wsp 文件。 但是，还必须将其激活，才能在 SharePoint 中使用。

6. 在“解决方案库”页上，选择 SharePoint 应用程序，然后在功能区上，选择“激活”按钮。 

7. 在“激活解决方案”对话框的功能区上，再次选择“激活”按钮。 

     “解决方案库”页上的“状态”列指示应用程序处于活动状态。 

## <a name="to-upgrade-a-sandboxed-sharepoint-solution-on-a-remote-sharepoint-server"></a>若要在远程 SharePoint 服务器上升级沙盒 SharePoint 解决方案
 如果已在远程服务器上发布沙盒 SharePoint 解决方案，则可以在对 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的应用程序进行更改后使用以下过程对其进行升级。

1. 重命名 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的 SharePoint 包。 要执行该操作，请在“解决方案资源管理器”中，打开包。 它显示在“包资源管理器”中。

2. 在“包资源管理器”的“名称”框中，将包名称更改为唯一名称。 

3. 保存项目。

4. 在“解决方案资源管理器”中，打开项目的快捷菜单，然后选择“发布”。

5. 在“发布”对话框中，选择“发布到 SharePoint 站点”选项按钮，如果保存解决方案的远程服务器的 URL 丢失了，则输入该 URL。 

6. 选择“发布后在浏览器中打开解决方案库页”选项按钮，以便在发布后查看“解决方案库”页中的解决方案列表。 

7. 选择 **“发布”** 按钮。

8. 如果需要进行用户身份验证，请登录到远程服务器。

     如果最近登录了远程服务器，则可能不需要进行身份验证。

     如果 SharePoint 服务器上仍然名称相同的较旧版本的应用程序，将会收到错误消息，提示 SharePoint 服务器上已存在具有相同名称的包。 在发布之前，必须先将包重命名为唯一名称。

9. 在 SharePoint 中选择新的应用程序，然后在功能区上，选择“升级”按钮。

10. 在“升级解决方案”对话框的功能区上，再次选择“升级”按钮。  “解决方案库”页上的“状态”列现在应指示应用程序处于活动状态。 

     如果已停用旧版本的解决方案，则会使用从旧解决方案保留的数据来升级新版本的解决方案，进而在 SharePoint 中激活新的解决方案。

## <a name="see-also"></a>另请参阅
- [如何：将 SharePoint 解决方案部署和发布到本地 SharePoint 站点](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)
- [创建 SharePoint 解决方案包](../sharepoint/creating-sharepoint-solution-packages.md)
- [如何：自定义 SharePoint 解决方案包](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [如何：使用包设计器在包中添加和删除功能和项](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
