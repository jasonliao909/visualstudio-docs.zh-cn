---
title: 指定部署更新的备用位置
description: 了解如何在部署清单中为 ClickOnce应用程序的更新指定备用位置。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160642"
---
# <a name="how-to-specify-an-alternate-location-for-deployment-updates"></a>如何：指定部署更新的备用位置
最初可以从 CD 或文件共享安装应用程序，但应用程序必须在 Web [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 上检查定期更新。 可以在部署清单中指定更新的备用位置，以便应用程序可以在初始安装后从 Web 更新自身。

> [!NOTE]
> 必须将应用程序配置为在本地安装，以使用此功能。 有关详细信息，请参阅[演练：手动](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)部署ClickOnce应用程序。 此外，如果从网络安装应用程序，设置备用位置会导致该位置同时用于初始安装和 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 所有后续更新。 如果在本地安装应用程序 (例如，从 CD) ，将使用原始介质执行初始安装，所有后续更新都将使用备用位置。

### <a name="specify-an-alternate-location-for-updates-by-using-mageuiexe-windows-forms-based-utility"></a>使用基于窗体的实用工具MageUI.exe (Windows指定更新的备用) 

1. 打开命令.NET Framework并键入：

     **MageUI.exe**

2. 在" **文件** "菜单上 **，选择"** 打开"以打开应用程序的部署清单。

3. 选择“部署选项”选项卡。

4. 在名为"启动 **位置"的** 文本框中，输入包含应用程序更新部署清单的目录的 URL。

5. 保存部署清单。

### <a name="specify-an-alternate-location-for-updates-by-using-mageexe"></a>使用 Mage.exe 指定更新的备用Mage.exe

1. 打开.NET Framework提示符。

2. 使用下列命令设置更新位置。 本示例中 *，HelloWorld.exe.application* 是应用程序清单的路径，该清单始终具有 .application 扩展名，也是将检查应用程序更新 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `http://adatum.com/Update/Path` 的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] URL。

    **Mage -Update HelloWorld.exe.application -ProviderUrl http： \/ /adatum.com/Update/Path**

3. 保存文件。

   > [!NOTE]
   > 现在，需要使用Mage.exe对 *文件进行重新签名*。 有关详细信息，请参阅[演练：手动](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)部署ClickOnce应用程序。

## <a name="net-framework-security"></a>.NET Framework 安全性
 如果从 CD 等脱机介质安装应用程序，并且计算机处于联机状态，则首先检查部署清单中 标记指定的 URL，以确定更新位置是否包含较新版本 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `<deploymentProvider>` 的应用程序。 如果安装，则直接从安装目录（而不是从初始安装目录）安装应用程序，公共语言运行时 (CLR) 使用 确定应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的信任级别 `<deploymentProvider>` 。 如果计算机处于脱机状态或无法访问，则从 CD 安装，并且 CLR 基于安装点授予信任;对于 CD 安装，这意味着应用程序将接收 `<deploymentProvider>` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 完全信任。 所有后续更新都将继承该信任级别。

 使用 的所有应用程序都应显式声明其应用程序清单中所需的权限，以便应用程序不会在不同的计算机上收到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `<deploymentProvider>` 不同级别的信任。

## <a name="see-also"></a>请参阅
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [ClickOnce部署清单](../deployment/clickonce-deployment-manifest.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)