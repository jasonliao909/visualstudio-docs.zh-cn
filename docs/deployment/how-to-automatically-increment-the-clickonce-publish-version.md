---
title: 自动递增 ClickOnce 发布版本
description: 了解如何使用 Visual Studio 禁用 ClickOnce 应用程序的修订号自动递增。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], incrementing publish version automatically
- Publish Version property, incrementing
- ClickOnce deployment, incrementing publish version automatically
- publishing, ClickOnce
ms.assetid: 686ab88a-6305-4914-a05b-fe269cc0ae1e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: c2f4db86a97743d8844ef7664d31cdf3649a14c7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665625"
---
# <a name="how-to-automatically-increment-the-clickonce-publish-version"></a>如何：自动递增 ClickOnce 发布版本

发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，更改 `Publish Version` 属性将导致应用程序作为更新发布。 默认情况下，Visual Studio 会在每次发布应用程序时自动递增 `Publish Version` 的 `Revision` 版本号。

可以在“项目设计器”的“发布”页上禁止该行为 。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="to-disable-automatically-incrementing-the-publish-version"></a>禁用发布版本的自动递增

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在“发布版本”部分中，清空“自动递增每个版本的修订号”复选框 。

## <a name="see-also"></a>另请参阅

- [如何：设置 ClickOnce 发布版本](../deployment/how-to-set-the-clickonce-publish-version.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)