---
title: 指定脱机或联机安装模式 (ClickOnce)
description: 了解如何为 ClickOnce 应用程序指定安装模式，该模式确定应用程序是可供脱机使用还是联机使用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, specifying install mode
- install mode
- online applications
- offline applications
- ClickOnce install mode
ms.assetid: 0aee5fc1-e966-4bda-9b8f-d9997aeaa779
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 68d51ae558c6bc40c632c680a76248b7ac1b4cb1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665866"
---
# <a name="how-to-specify-the-clickonce-offline-or-online-install-mode"></a>如何：指定 ClickOnce 脱机或联机安装模式
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的 `Install Mode` 确定应用程序是可供脱机使用还是联机使用。 选择“应用程序仅可联机使用”时，用户必须有权访问 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 发布位置（网页或文件共享）才能运行该应用程序。 选择“应用程序也可脱机使用”时，应用程序会将条目添加到“开始”菜单和“添加或删除程序”对话框；用户能够在未连接时运行应用程序。

可以在“项目设计器”的“发布”页上设置 `Install Mode`。

> [!NOTE]
> 还可通过使用发布向导来设置 `Install Mode`。 有关详细信息，请参阅[操作说明：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

### <a name="to-make-a-clickonce-application-available-online-only"></a>使 ClickOnce 应用程序仅可联机使用

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在“安装模式和设置”区域中，单击“应用程序仅可联机使用”选项按钮。

### <a name="to-make-a-clickonce-application-available-online-or-offline"></a>使 ClickOnce 应用程序可供联机或脱机使用

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在“安装模式和设置”区域中，单击“应用程序也可脱机使用”选项按钮。

     安装后，应用程序会将条目添加到“开始”菜单和控制面板中的“添加或删除程序”。

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)