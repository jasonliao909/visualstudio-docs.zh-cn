---
title: 发布 ClickOnce 应用程序 | Microsoft Docs
description: 了解如何使用发布向导首次发布 ClickOnce 应用程序。 在项目设计器中的“发布”页上进行后续更改。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.Dialog.Options
- Microsoft.VisualStudio.Publish.ClickOnceProvider.PublishWizard.Help
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, publishing
- ClickOnce applications, publishing
- applications [Visual Studio], ClickOnce deployment
- deploying applications [ClickOnce], publishing ClickOnce applications
ms.assetid: eb6dfe79-f54c-4331-8e36-073688e70973
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 4e4537670ef43ceb7379adb29390e316f74243c8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671809"
---
# <a name="publish-clickonce-applications"></a>发布 ClickOnce 应用程序
首次发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，可以使用“发布向导”设置发布属性。 只有几个属性在向导中可用，所有其他属性均设置为其默认值。

 可以在“项目设计器”的“发布”页面上对发布属性进行后续更改。

## <a name="publish-wizard"></a>发布向导
 你可以使用“发布向导”进行基本设置以发布应用程序。 这包括以下发布属性：

- 发布文件夹所在的位置 - Visual Studio 将从其复制文件的位置（本地计算机、网络文件共享、FTP 服务器或网站）

- 安装文件夹所在的位置 - 最终用户将从其进行安装的位置（网络文件共享、FTP 服务器、网站、CD/DVD）

- 联机或脱机可用性 - 最终用户在有或没有网络连接的情况下访问应用程序

- 更新频率 - 应用程序检查新更新的频率。

  有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

## <a name="publish-page"></a>“发布”页面
 “项目设计器”  上的“发布”  页面用于针对 ClickOnce 部署配置属性。 下表列出主题。

|标题|说明|
|-----------|-----------------|
|[如何：指定 Visual Studio 复制文件的位置](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)|介绍如何设置 Visual Studio 放置应用程序文件和清单的位置。|
|[如何：指定最终用户将从中进行安装的位置](../deployment/how-to-specify-the-location-where-end-users-will-install-from.md)|介绍如何设置用户可以下载和安装应用程序的位置。|
|[如何：指定 ClickOnce 脱机或联机安装模式](../deployment/how-to-specify-the-clickonce-offline-or-online-install-mode.md)|介绍如何设置应用程序联机或脱机可用。|
|[如何：设置 ClickOnce 发布版本](../deployment/how-to-set-the-clickonce-publish-version.md)|介绍如何设置 ClickOnce“发布版本”属性，该属性确定发布的应用程序是否被视为更新。|
|[如何：自动递增 ClickOnce 发布版本](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)|介绍如何在每次发布应用程序时自动递增“发布版本”的版本号。|

 有关详细信息，请参阅[“项目设计器”->“发布”页](../ide/reference/publish-page-project-designer.md)

### <a name="application-files-dialog-box"></a>“应用程序文件”对话框
 在此对话框中，你可以指定如何在项目中对文件分类，以实现发布、动态下载和更新。 它包含一个网格，该网格中列出默认未排除或有下载组的项目文件。

 若要排除文件，请将文件标记为数据文件或系统必备，并创建文件组以便在 Visual Studio UI 中进行条件安装，请参阅[如何：指定通过 ClickOnce 发布的文件](../deployment/how-to-specify-which-files-are-published-by-clickonce.md)。 你还可以通过使用 Mage.exe 标记数据文件。 有关详细信息，请参阅[如何：将数据文件包括到 ClickOnce 应用程序中](../deployment/how-to-include-a-data-file-in-a-clickonce-application.md)。

### <a name="prerequisites-dialog-box"></a>“系统必备”对话框
 此对话框指定要安装的必备组件以及其安装方式。 有关详细信息，请参阅[如何：与 ClickOnce 应用程序一起安装系统必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)和[“系统必备”对话框](../ide/reference/prerequisites-dialog-box.md)。

### <a name="application-updates-dialog-box"></a>“应用程序更新”对话框
 此对话框指定应如何检查应用程序安装的更新。 有关详细信息，请参阅[如何：管理 ClickOnce 应用程序的更新](../deployment/how-to-manage-updates-for-a-clickonce-application.md)。

### <a name="publish-options-dialog-box"></a>“发布选项”对话框
 “发布选项”对话框指定应用程序的部署选项。

|标题|说明|
|-|-|
|[如何：更改 ClickOnce 应用程序的发布语言](../deployment/how-to-change-the-publish-language-for-a-clickonce-application.md)|介绍如何指定与本地化版本匹配的语言和区域性。|
|[如何：指定 ClickOnce 应用程序的“开始”菜单名称](../deployment/how-to-specify-a-start-menu-name-for-a-clickonce-application.md)|介绍如何更改 ClickOnce 应用程序的显示名称。|
|[如何：指定技术支持链接](../deployment/how-to-specify-a-link-for-technical-support.md)|介绍如何设置“支持 URL”属性，该属性确定用户可以转至以获取应用程序相关信息的网页或文件共享。|
|[如何：为 ClickOnce 部署中的各个系统必备项指定一个支持 URL](../deployment/how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment.md)|演示如何手动更改应用程序清单以包括各系统必备单独的支持 URL。|
|[如何：指定 ClickOnce 应用程序的发布页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)|介绍如何生成默认网页 (publish.htm) 并随应用程序一起发布。|
|[如何：自定义 ClickOnce 的默认网页](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)|介绍如何自定义自动生成并随应用程序一起发布的网页。|
|[如何：为 CD 安装启用自动启动](../deployment/how-to-enable-autostart-for-cd-installations.md)|介绍如何启用“自动启动”以便在插入媒体时自动启动 ClickOnce 应用程序。|

## <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[如何：为 ClickOnce 应用程序创建文件关联](../deployment/how-to-create-file-associations-for-a-clickonce-application.md)|介绍如何向 ClickOnce 应用程序添加文件名称扩展支持。|
|[如何：在联机 ClickOnce 应用程序中检索查询字符串信息](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)|演示如何检索在用于运行 ClickOnce 应用程序的 URL 中传递的参数。|
|[如何：使用设计器禁用 ClickOnce 应用程序的 URL 激活](../deployment/how-to-disable-url-activation-of-clickonce-applications-by-using-the-designer.md)|介绍如何强制用户通过使用设计器从“开始”菜单启动应用程序。|
|[如何：禁用 ClickOnce 应用程序的 URL 激活](../deployment/how-to-disable-url-activation-of-clickonce-applications.md)|介绍如何强制用户从“开始”菜单启动应用程序。|
|[演练：在设计器中使用 ClickOnce 部署 API 按需下载程序集](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer.md)|说明如何仅在应用程序首次使用程序集时通过设计器进行下载。|
|[演练：使用 ClickOnce 部署 API 按需下载程序集](../deployment/walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api.md)|说明如何仅在应用程序首次使用程序集时进行下载。|
|[演练：使用 ClickOnce 部署 API 按需下载附属程序集](../deployment/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api.md)|介绍如何将附属程序集标记为可选，以及如何下载客户端计算机针对其当前区域性设置而需要的程序集。|
|[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)|说明如何使用 .NET Framework 实用程序部署 ClickOnce 应用程序。|
|[演练：手动部署不需要重新签名并且保留署名信息的 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)|说明如何使用 .NET Framework 实用程序在不对清单进行重新签名的情况下部署 ClickOnce 应用程序。|
|[如何：将项目配置为面向平台](../ide/how-to-configure-projects-to-target-platforms.md)|说明如何通过更改项目中的“目标 CPU”或“平台目标”属性发布 64 位处理器。|
|[演练：启用 ClickOnce 应用程序以在多个 .NET Framework 版本上运行](/previous-versions/dd996998(v=vs.100))|说明如何启用 ClickOnce 应用程序以在多个版本的 NET Framework 上安装并运行。|
|[演练：为 ClickOnce 应用程序创建自定义安装程序](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md)|说明如何创建自定义安装程序以安装 ClickOnce 应用程序。|
|[如何：发布启用了视觉样式的 WPF 应用程序](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)|提供分步说明以解决在尝试发布已启用视觉样式的 WPF 应用程序时出现的错误。|

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce 参考](../deployment/clickonce-reference.md)