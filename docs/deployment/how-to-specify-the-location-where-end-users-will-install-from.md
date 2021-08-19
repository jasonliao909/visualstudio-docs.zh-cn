---
title: 指定最终用户安装的位置
description: 了解如何设置 "安装 URL" 属性，该属性是用于安装的已发布 ClickOnce 应用程序的宿主。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160603"
---
# <a name="how-to-specify-the-location-where-end-users-will-install-from"></a>如何：指定最终用户将从中进行安装的位置

在发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，用户下载和安装应用程序的位置不一定是最初发布应用程序的位置。 例如，在某些组织中，开发人员可能会将应用程序发布到暂存服务器，然后管理员会将该应用程序移动到 Web 服务器。

在这种情况下，可以使用 `Installation URL` 属性来指定用户下载应用程序时将使用的 Web 服务器。 这是必需的，以便应用程序清单知道在何处查找更新。

`Installation URL`可以在 **Project 设计器** 的 "**发布**" 页上设置属性。

> [!NOTE]
> `Installation URL`还可以使用 **发布向导** 来设置属性。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

### <a name="to-specify-an-installation-url"></a>指定安装 URL

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在 "安装 URL" 字段中，使用格式输入完全限定的 URL `https://www.contoso.com/ApplicationName` ，或使用格式的 UNC 路径输入安装位置 `\Server\ApplicationName` 。

## <a name="see-also"></a>请参阅
- [如何：指定 Visual Studio 复制文件的位置](../deployment/how-to-specify-where-visual-studio-copies-the-files.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)