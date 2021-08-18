---
title: 为 CD 安装启用自动启动|Microsoft Docs
description: 了解如何使用可移动媒体（如 CD-ROM 或 DVD-ROM）ClickOnce应用程序时启用 AutoStart。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, AutoStart
- ClickOnce deployment, installation on CD or DVD
- deploying applications [ClickOnce], installation on CD or DVD
ms.assetid: caaec619-900c-4790-90e3-8c91f5347635
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: f16def763bebca4cc91b902d1f9202c6a6fdaede
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127917"
---
# <a name="how-to-enable-autostart-for-cd-installations"></a>如何：为 CD 安装启用自动启动
通过可移动媒体（如 CD-ROM 或 DVD-ROM）部署应用程序时，可以启用 ，以便插入媒体时自动 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `AutoStart` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 启动应用程序。

 `AutoStart`可以在设计器 **的"** 发布 **"Project启用**。

### <a name="to-enable-autostart"></a>启用自动启动

1. 在 "属性"**中解决方案资源管理器**，在 Project菜单上单击 **"** 属性 **"。**

2. 单击 **“发布”** 选项卡。

3. 单击“选项”  按钮。

     将显示 **"发布选项** "对话框。

4. 单击“部署”。

5. 选中" **对于 CD 安装，在插入 CD 时自动启动安装程序** "复选框。

     发布 *应用程序时，Autorun.inf* 文件将复制到发布位置。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)