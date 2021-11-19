---
title: 设置 ClickOnce 发布版本 | Microsoft Docs
description: 了解如何设置 ClickOnce 发布版本属性，该属性决定应用程序是否是更新。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, setting publish version
- publishing, ClickOnce
- Publish Version property
ms.assetid: 06f15504-6385-40a6-b01d-cd90ca36dc73
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 39c126a1e2758bbbbc24c0f6ef5fa9b6310669eb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601007"
---
# <a name="how-to-set-the-clickonce-publish-version"></a>如何：设置 ClickOnce 发布版本
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `Publish Version` 属性决定是否将要发布的应用程序视为更新。 每次版本递增时，应用程序都将作为更新发布。

 可以在“项目设计器”的“发布”页上设置 `Publish Version` 属性 。

> [!NOTE]
> 有一个项目选项会在每次发布应用程序时自动递增 `Publish Version` 属性；默认情况下启用此选项。 有关详细信息，请参阅 [如何自动递增 ClickOnce 发布版本](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)。

### <a name="to-change-the-publish-version"></a>更改发布版本

1. 在“解决方案资源管理器” 中选择一个项目，然后在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在“发布版本”字段中，递增“主版本号”、“次版本号”、“内部版本号”或“修订”版本号    。

    > [!NOTE]
    > 切勿递减版本号；这样做可能会导致不可预知的更新行为。

## <a name="see-also"></a>另请参阅
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [如何：自动递增 ClickOnce 发布版本](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)