---
title: 使用 ClickOnce 部署 API 的自动应用更新
description: 了解如何在 ClickOnce 中编写代码以使用 ApplicationDeployment 类根据事件（如用户请求）检查更新。
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
ms.openlocfilehash: e098fb606b5d315ffc377d88ddfe9cbc1b665ec5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665615"
---
# <a name="how-to-check-for-application-updates-programmatically-using-the-clickonce-deployment-api"></a>如何：使用 ClickOnce 部署 API 以编程方式检查应用程序更新
ClickOnce 提供两种方法来更新部署后的应用程序。 在第一种方法中，可以将 ClickOnce 部署配置为按特定时间间隔自动检查更新。 在第二种方法中，可以编写代码以使用 <xref:System.Deployment.Application.ApplicationDeployment> 类根据事件（如用户请求）检查更新。

 以下过程显示了用于执行编程更新的一些代码，还介绍了如何配置 ClickOnce 部署以启用编程更新检查。

 若要以编程方式更新 ClickOnce 应用程序，必须指定更新位置。 这有时称为部署提供程序。 有关设置此属性的详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

> [!NOTE]
> 还可使用下面所述的技术从一个位置部署应用程序，但从另一个位置更新应用程序。 有关详细信息，请参阅[如何：指定部署更新的其他位置](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)。

### <a name="to-check-for-updates-programmatically"></a>以编程方式检查更新

1. 使用首选的命令行或可视化工具创建新的 Windows 窗体应用程序。

2. 创建任何按钮、菜单项或其他用户界面项，供用户选择以检查更新。 从该项的事件处理程序中，调用以下方法来检查和安装更新。

    :::code language="csharp" source="../snippets/csharp/VS_Snippets_Winforms/ClickOnceAPI/CS/Form1.cs" id="Snippet6":::
    :::code language="cpp" source="../snippets/cpp/VS_Snippets_Winforms/ClickOnceAPI/cpp/form1.cpp" id="Snippet6":::
    :::code language="vb" source="../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceAPI/VB/Form1.vb" id="Snippet6":::

3. 编译应用程序。

### <a name="use-mageexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>使用 Mage.exe 来部署以编程方式检查更新的应用程序

- 按照[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)中的说明，使用 Mage.exe 部署应用程序。 调用 Mage.exe生成部署清单时，请确保使用命令行开关 `providerUrl`，并指定 ClickOnce 应在其中检查更新的 URL。 例如，如果应用程序从 `http://www.adatum.com/MyApp` 进行更新，用于生成部署清单的调用可能如下所示：

    ```cmd
    mage -New Deployment -ToFile WindowsFormsApp1.application -Name "My App 1.0" -Version 1.0.0.0 -AppManifest 1.0.0.0\MyApp.manifest -providerUrl http://www.adatum.com/MyApp/MyApp.application
    ```

### <a name="using-mageuiexe-to-deploy-an-application-that-checks-for-updates-programmatically"></a>使用 MageUI.exe 来部署以编程方式检查更新的应用程序

- 按照[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)中的说明，使用 Mage.exe 部署应用程序。 在“部署选项”选项卡上，将“开始位置”字段设置为 ClickOnce 应检查更新的应用程序清单 。 在“更新选项”选项卡上，清除“此应用程序应检查更新”复选框 。

## <a name="net-framework-security"></a>.NET Framework 安全性
 应用程序必须具有完全信任权限才能使用编程更新。

## <a name="see-also"></a>另请参阅
- [如何：指定部署更新的其他位置](../deployment/how-to-specify-an-alternate-location-for-deployment-updates.md)
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)