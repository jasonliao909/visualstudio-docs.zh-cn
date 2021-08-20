---
title: 部署ClickOnce应用而无需重新签名
description: 了解如何从多个ClickOnce位置部署应用程序，而无需重新签名或更改ClickOnce清单。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160850"
---
# <a name="deploy-clickonce-applications-for-testing-and-production-servers-without-resigning"></a>在不ClickOnce的情况下为测试和生产服务器部署应用程序
本文介绍 .NET Framework 版本 3.5 中引入的 ClickOnce 功能，该功能允许从多个网络位置部署 ClickOnce 应用程序，而无需重新签名或更改 ClickOnce 清单。

> [!NOTE]
> 放弃仍是部署新版本的应用程序的首选方法。 如果可能，请使用恢复方法。 有关详细信息，请参阅Mage.exe[  (清单生成和编辑工具) 。 ](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)

 第三方开发人员和 ISV 可以选择启用此功能，使客户可以更轻松地更新其应用程序。 此功能可用于以下情况：

- 更新应用程序时，不用于首次安装应用程序。

- 计算机上只有一个应用程序配置时。 例如，如果将应用程序配置为指向两个不同的数据库，则不能使用此功能。

## <a name="exclude-deploymentprovider-from-deployment-manifests"></a>从部署清单中排除 deploymentProvider
 在 .NET Framework 2.0 和 .NET Framework 3.0 中，安装在系统上用于脱机可用性的任何 ClickOnce 应用程序都必须在其部署清单中列出 。 `deploymentProvider` 通常称为更新位置;它是应用程序更新ClickOnce `deploymentProvider` 的位置。 此要求以及应用程序发布者对部署进行签名的需求使得公司难以从供应商ClickOnce第三方更新应用程序。 这也使得从同一网络上多个位置部署同一应用程序更加困难。

 在 .NET Framework 3.5 ClickOnce中对 ClickOnce 所做的更改后，第三方可以将 ClickOnce 应用程序提供给另一个组织，然后，该组织可以在其自己的网络上部署该应用程序。

 若要利用此功能，应用程序开发人员ClickOnce其 `deploymentProvider` 部署清单中排除。 此要求意味着在使用 Mage.exe 创建 `-providerUrl` 部署清单时必须排除 参数。 或者，如果要使用 MageUI.exe 生成部署清单，必须确保"应用程序清单"选项卡上的"启动位置"文本框留空。 

## <a name="deploymentprovider-and-application-updates"></a>deploymentProvider 和应用程序更新
 从 .NET Framework 3.5 开始，不再需要在部署清单中指定 ，以便为联机和脱机使用部署 ClickOnce `deploymentProvider` 应用程序。 此更改支持需要自己打包和签名部署的方案，但允许其他公司通过其网络部署应用程序。

 需要记住的重要一点是，排除 的应用程序在更新期间无法更改其安装位置，除非它们再次提供包含 标记 `deploymentProvider` `deploymentProvider` 的更新。

 下面是两个示例来阐明这一点。 第一个示例发布一ClickOnce没有标记的应用程序，并要求用户 `deploymentProvider` 从 安装 `http://www.adatum.com/MyApplication/` 它。 如果决定从 发布应用程序的下一个更新，则你无法将其表示在 驻留 `http://subdomain.adatum.com/MyApplication/` 在 的部署清单中 `http://www.adatum.com/MyApplication/` 。 可以执行两项操作之一：

- 告知用户卸载以前的版本，然后从新位置安装新版本。

- 在 中包含一 `http://www.adatum.com/MyApplication/` 个更新，其中包括 `deploymentProvider` 指向 的 `http://www.adatum.com/MyApplication/` 。 然后，稍后发布指向 的另 `deploymentProvider` 一个更新 `http://subdomain.adatum.com/MyApplication/` 。

  第二个示例发布指定 ClickOnce 的应用程序， `deploymentProvider` 然后决定将其删除。 将不带 的新版本下载到客户端后，在发布已还原的应用程序版本之前，无法重定向用于 `deploymentProvider` 更新 `deploymentProvider` 的路径。 与第一个示例一样， 最初必须指向 `deploymentProvider` 当前更新位置，而不是新位置。 在这种情况下，如果尝试插入引用 的 `deploymentProvider` `http://subdomain.adatum.com/MyApplication/` ，则下一次更新将失败。

## <a name="create-a-deployment"></a>创建部署
 有关创建可以从不同网络位置部署的部署的分步指南，请参阅演练：手动部署不需要重新签名并保留品牌信息的[ClickOnce](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)应用程序。

## <a name="see-also"></a>请参阅
- [*Mage.exe(清单生成和编辑工具)*](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [*MageUI.exe(清单生成和编辑工具，* 图形客户端)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
