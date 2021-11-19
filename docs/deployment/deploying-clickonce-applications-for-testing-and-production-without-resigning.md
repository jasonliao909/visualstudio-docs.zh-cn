---
title: 在不重新签名的情况下部署 ClickOnce 应用
description: 了解如何在不重新签名或更改 ClickOnce 清单的情况下，从多个网络位置部署 ClickOnce 应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, deploying without resigning
- ClickOnce deployment, without resigning
- application updates, ClickOnce
- update location [ClickOnce]
- deploymentProvider tag
- manifests [ClickOnce]
ms.assetid: 1218a98d-1ad5-4eef-95dd-0e0b3c44168c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 19eb91f9becdeeddbf5f5436a4f0b3b7da59da77
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665645"
---
# <a name="deploy-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>在不重新签名的情况下为测试服务器和生产服务器部署 ClickOnce 应用程序
本文介绍了 .NET Framework 版本 3.5 中引入的 ClickOnce 功能，该功能支持在不重新签名或更改 ClickOnce 清单的情况下从多个网络位置部署 ClickOnce 应用程序。

> [!NOTE]
> 重新签名仍是部署新版应用程序的首选方法。 尽可能使用重新签名方法。 有关详细信息，请参阅 [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)。

 第三方开发人员和 ISV 可选择加入此功能，这样客户就可以更轻松地更新他们的应用程序。 在以下情况下，可使用此功能：

- 更新应用程序时（不适用于首次安装应用程序）。

- 当计算机上只有一个应用程序配置时。 例如，如果应用程序配置为指向两个不同的数据库，则不能使用此功能。

## <a name="exclude-deploymentprovider-from-deployment-manifests"></a>从部署清单中排除 deploymentProvider
 在 .NET Framework 2.0 和 .NET Framework 3.0 中，安装在系统上以供脱机使用的任何 ClickOnce 应用程序都必须在其部署清单中列出 `deploymentProvider`。 `deploymentProvider` 通常称为更新位置；它是 ClickOnce 检查应用程序更新的位置。 此要求以及应用程序发布者需要对部署进行签名，使公司很难从供应商或其他第三方更新 ClickOnce 应用程序。 这也使得从同一网络上的多个位置部署相同的应用程序变得更加困难。

 通过在 .NET Framework 3.5 中对 ClickOnce 所做的更改，第三方可以向另一个组织提供 ClickOnce 应用程序，然后该组织可以在自己的网络上部署该应用程序。

 为了利用此功能，ClickOnce 应用程序的开发人员必须从其部署清单中排除 `deploymentProvider`。 此要求意味着在使用 Mage.exe 创建部署清单时必须排除 `-providerUrl` 参数。 如果使用 MageUI.exe 生成部署清单，也必须确保“应用程序清单”选项卡上的“启动位置”文本框留空 。

## <a name="deploymentprovider-and-application-updates"></a>deploymentProvider 和应用程序更新
 从 .NET Framework 3.5 开始，无需在部署清单中指定 `deploymentProvider` 便可部署供联机和脱机使用的 ClickOnce 应用程序。 此更改支持需要自己打包和签署部署的场景，但允许其他公司通过网络部署应用程序。

 务必要记住的是，排除 `deploymentProvider` 的应用程序无法在更新期间更改其安装位置，直到它们再次发布包含 `deploymentProvider` 标记的更新。

 可通过以下两个示例来说明这一点。 在第一个示例中，你发布了一个没有 `deploymentProvider` 标记的 ClickOnce 应用程序，并要求用户从 `http://www.adatum.com/MyApplication/` 安装该应用程序。 如果决定要从 `http://subdomain.adatum.com/MyApplication/` 发布应用程序的下一次更新，则无法在位于 `http://www.adatum.com/MyApplication/` 中的部署清单中表明这一点。 可以执行以下任一操作：

- 告知用户卸载以前的版本，并从新位置安装新版本。

- 包括 `http://www.adatum.com/MyApplication/` 上的更新，其中包含指向 `http://www.adatum.com/MyApplication/` 的 `deploymentProvider`。 然后，稍后发布另一个更新，其中包含指向 `http://subdomain.adatum.com/MyApplication/` 的 `deploymentProvider`。

  在第二个示例中，你发布了一个指定 `deploymentProvider` 的 ClickOnce 应用程序，然后你决定将其删除。 将不带 `deploymentProvider` 的新版本下载到客户端后，在发布还原了 `deploymentProvider` 的应用程序版本之前，不能重定向用于更新的路径。 与第一个示例一样，`deploymentProvider` 最初必须指向当前更新位置，而不是新位置。 在这种情况下，如果尝试插入引用 `http://subdomain.adatum.com/MyApplication/` 的 `deploymentProvider`，则下一次更新将失败。

## <a name="create-a-deployment"></a>创建部署
 有关如何创建可从不同网络位置部署的部署的分步指南，请参阅[演练：手动部署不需要重新签名并保留品牌打造信息的 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)。

## <a name="see-also"></a>另请参阅
- [*Mage.exe*（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [*MageUI.exe*（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
