---
title: 指定最终用户的安装位置
description: 了解如何设置"安装 URL"属性，该属性是托管ClickOnce应用程序的发布 URL 属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying an installation URL
- URLs, specifying an installation URL
- installation, specifying installation an URL
- Installation URL property
ms.assetid: 04a804bf-ed55-4a7a-a1e6-f63ed99c0276
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: dae59aa3fb9bde3d2ed43cf7d8c41da4079cf408
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664661"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>如何：指定最终用户将从中进行安装的位置

发布应用程序时，用户下载和安装应用程序的位置不一定是最初 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 发布应用程序的位置。 例如，在某些组织中，开发人员可能会将应用程序发布到过渡服务器，然后管理员将应用程序移到 Web 服务器。

在这种情况下，可以使用 属性指定用户要下载应用程序的 `Installation URL` Web 服务器。 这是必需的，以便应用程序清单知道在何处查找更新。

`Installation URL`可以在设计器 的"发布"页上Project **属性**。

> [!NOTE]
> `Installation URL`还可使用 **PublishWizard 设置 属性**。 有关详细信息，请参阅[如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

### <a name="to-specify-an-installation-url"></a>指定安装 URL

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在"安装 URL"字段中，使用格式 为 的完全限定 URL 或格式 `https://www.contoso.com/ApplicationName` 为 的 UNC 路径输入安装位置 `\Server\ApplicationName` 。

## <a name="see-also"></a>另请参阅
- [如何：指定Visual Studio位置](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)
- [发布ClickOnce应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)