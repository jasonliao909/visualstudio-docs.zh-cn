---
title: ClickOnce 如何执行应用程序更新 | Microsoft Docs
description: 了解 ClickOnce 如何使用文件版本信息来决定是否更新应用程序。 ClickOnce 使用文件修补来避免下载时出现冗余。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- updates, ClickOnce
- ClickOnce deployment, updates
- deploying applications [ClickOnce], application updates
ms.assetid: d54313c2-cf0c-420d-b151-99953a95f0bb
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 046348ed2f6e8425434291454bb2162aac5c0f82
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665628"
---
# <a name="how-clickonce-performs-application-updates"></a>ClickOnce 如何执行应用程序更新
ClickOnce 使用应用程序部署清单中指定的文件版本信息决定是否更新应用程序文件。 更新开始后，ClickOnce 使用“文件修补”技术来避免应用程序文件的冗余下载。

## <a name="file-patching"></a>文件修补
 更新应用程序时，ClickOnce 不会下载新版本应用程序的所有文件，除非文件发生了更改。 相反，它会将当前应用程序的应用程序清单中指定的文件的哈希签名与新版本清单中的签名进行比较。 如果文件签名不同，ClickOnce 将下载新版本。 如果签名匹配，则文件在两个版本之间未发生变更。 在这种情况下，ClickOnce 将复制现有文件，并在应用程序的新版本中使用它。 此方法可防止 ClickOnce 再次下载整个应用程序，即使只有一个或两个文件发生了更改。

 文件修补还适用于使用 <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroup%2A> 和 <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroupAsync%2A> 方法按需下载的程序集。

 如果使用 Visual Studio 编译应用程序，则每当你重新生成整个项目时，它都会为所有文件生成新哈希签名。 在这种情况下，所有程序集都将下载到客户端，尽管可能只有几个程序集发生了更改。

 文件修补对标记为数据并存储在数据目录中的文件不起作用。 无论文件的哈希签名如何，始终都会下载这些文件。 有关数据目录的详细信息，请参阅[在 ClickOnce 应用程序中访问本地数据和远程数据](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)。

## <a name="see-also"></a>另请参阅
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)