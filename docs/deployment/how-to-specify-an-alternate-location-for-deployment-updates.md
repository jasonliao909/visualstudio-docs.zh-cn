---
title: 指定部署更新的备用位置
description: 了解如何在部署清单中为 ClickOnce 应用程序指定更新的备用位置。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, updates
- deployment update, alternative locations
ms.assetid: 7faacd35-2638-492d-80f6-6b57e5f820de
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 9c9db27ae54519c56a2c8f7c60454a823c59dfff
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665861"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>如何：指定部署更新的备用位置
你可以首先从 CD 或文件共享安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，但是应用程序必须检查 Web 上的定期更新。 在部署清单中指定更新的备用位置，以便应用程序在初始安装后可以从 Web 进行自我更新。

> [!NOTE]
> 应用程序必须配置为本地安装才能使用此功能。 有关详细信息，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。 此外，如果在网络中安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，则设置备用位置会导致 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 在初始安装和所有后续更新中使用该位置。 如果在本地安装应用程序（例如，从 CD），则使用原始媒体执行初始安装，并且所有后续更新都将使用备用位置。

### <a name="specify-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>使用 MageUI.exe（基于 Windows 窗体的实用工具）指定更新的备用位置

1. 打开 .NET Framework 命令提示符和类型：

     **MageUI.exe**

2. 在“文件”菜单上，选择“打开”以打开应用程序的部署清单 。

3. 选择“部署选项”选项卡。

4. 在名为“启动位置”的文本框中，输入将包含应用程序更新的部署清单的目录的 URL。

5. 保存部署清单。

### <a name="specify-an-alternate-location-for-updates-by-using-mageexe"></a>使用 Mage.exe 指定更新的备用位置

1. 打开 .NET Framework 命令提示符。

2. 使用以下命令设置更新位置。 此示例中，HelloWorld.exe.application 是 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单的路径，该清单始终具有 .application 扩展名，`http://adatum.com/Update/Path` 是 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 用于检查应用程序更新的 URL。

    Mage -Update HelloWorld.exe.application -ProviderUrl http:\//adatum.com/Update/Path

3. 保存文件。

   > [!NOTE]
   > 现在，需要使用 Mage.exe 重新签署文件。 有关详细信息，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

## <a name="net-framework-security"></a>.NET Framework 安全性
 如果从脱机媒体（如 CD）安装应用程序，并且计算机处于联机状态，则 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 首先会检查部署清单中的 `<deploymentProvider>` 标记所指定的 URL，以确定更新位置是否包含应用程序的最新版本。 如果包含，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 将直接从该位置安装应用程序，而不是从初始安装目录中安装，公共语言运行时 (CLR) 将使用 `<deploymentProvider>` 确定应用程序的信任级别。 如果计算机处于脱机状态或 `<deploymentProvider>` 无法访问，则会从 CD 安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]，并且 CLR 将根据安装点授予信任；对于 CD 安装，这意味着应用程序将获得完全信任。 所有后续更新都将继承该信任级别。

 使用 `<deploymentProvider>` 的所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序应在其应用程序清单中显式声明所需的权限，以便应用程序不会在不同的计算机上收到不同的信任级别。

## <a name="see-also"></a>另请参阅
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)