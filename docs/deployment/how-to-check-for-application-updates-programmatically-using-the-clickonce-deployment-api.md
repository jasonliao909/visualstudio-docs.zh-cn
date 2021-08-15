---
title: 使用 ClickOnce 部署 API 自动进行的应用更新
description: 了解如何在 ClickOnce 中编写代码，该代码使用 microsoft.biztalk.applicationdeployment.engine.dll 类基于事件（例如用户请求）检查更新。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- application updates
ms.assetid: 1a886310-67c8-44e5-a382-c2f0454f887d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: e8440b6d5b3d83138183c368525486d0cad3778be9aee47b4c519b0ac563f461
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121435525"
---
# <a name="how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api"></a>如何：使用 ClickOnce 部署 API 以编程方式检查应用程序更新
ClickOnce 提供了两种方法，用于在部署应用程序后对其进行更新。 在第一种方法中，可以将 ClickOnce 部署配置为在特定的时间间隔自动检查更新。 在第二种方法中，可以编写使用类的代码 <xref:System.Deployment.Application.ApplicationDeployment> ，以根据事件（例如用户请求）检查更新。

 下面的过程演示了一些用于执行编程更新的代码，还介绍了如何配置 ClickOnce 部署以启用编程更新检查。

 若要以编程方式更新 ClickOnce 应用程序，必须指定更新的位置。 这有时称为部署提供程序。 有关设置此属性的详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

> [!NOTE]
> 你还可以使用下面所述的技术从一个位置部署你的应用程序，但从另一个位置进行更新。 有关详细信息，请参阅 [如何：指定部署更新的备用位置](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)。

### <a name="to-check-for-updates-programmatically"></a>以编程方式检查更新

1. 使用首选的命令行或视觉工具创建新的 Windows 窗体应用程序。

2. 创建希望用户选择用于检查更新的任何按钮、菜单项或其他用户界面项。 从该项的事件处理程序中，调用以下方法来检查和安装更新。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceAPI/CS/Form1.cs" id="Snippet6":::
    :::code language="cpp" source="../snippets/cpp/VS_Snippets_Winforms/ClickOnceAPI/cpp/form1.cpp" id="Snippet6":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceAPI/VB/Form1.vb" id="Snippet6":::

3. 编译你的应用程序。

### <a name="use-mageexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>使用 Mage.exe 部署以编程方式检查更新的应用程序

- 按照[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)中所述的步骤，按照有关使用 Mage.exe 部署应用程序的说明进行操作。 在调用 Mage.exe 生成部署清单时，请确保使用命令行开关 `providerUrl` ，并指定 ClickOnce 应检查更新的 URL。 例如，如果你的应用程序将从进行更新 `http://www.adatum.com/MyApp` ，则调用以生成部署清单可能如下所示：

    ```cmd
    mage -New Deployment -ToFile WindowsFormsApp1.application -Name "My App 1.0" -Version 1.0.0.0 -AppManifest 1.0.0.0\MyApp.manifest -providerUrl http://www.adatum.com/MyApp/MyApp.application
    ```

### <a name="using-mageuiexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>使用 MageUI.exe 部署以编程方式检查更新的应用程序

- 按照[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)中所述的步骤，按照有关使用 Mage.exe 部署应用程序的说明进行操作。 在 "**部署选项**" 选项卡上，将 "**开始位置**" 字段设置为应用程序清单 ClickOnce 应检查更新。 在 " **更新选项** " 选项卡上，清除 " **此应用程序应检查更新** " 复选框。

## <a name="net-framework-security"></a>.NET Framework 安全性
 应用程序必须具有完全信任权限才能使用编程更新。

## <a name="see-also"></a>另请参阅
- [如何：指定部署更新的备用位置](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)