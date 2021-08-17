---
title: 设置ClickOnce发布版本|Microsoft Docs
description: 了解如何设置"ClickOnce版本"属性，该属性确定应用程序是否是更新。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089896"
---
# <a name="how-to-set-the-clickonce-publish-version"></a>如何：设置 ClickOnce 发布版本
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `Publish Version` 属性确定是否将发布的应用程序视为更新。 每次版本递增时，应用程序都将作为更新发布。

 可以在 `Publish Version` 设计器 的"发布"页上Project **属性**。

> [!NOTE]
> 有一个项目选项会在每次发布应用程序时自动递增属性;默认情况下 `Publish Version` 启用此选项。 有关详细信息，请参阅[如何：自动递增发布ClickOnce版本](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)。

### <a name="to-change-the-publish-version"></a>更改发布版本

1. 在 "属性"**中解决方案资源管理器**，在 Project菜单上单击 **"** 属性 **"。**

2. 单击 **“发布”** 选项卡。

3. 在 **"发布版本"** 字段中，递增 **主** 版本号、次要版本号、生成 **版本号或修订** 版本号。 

    > [!NOTE]
    > 切勿减少版本号;这样做可能会导致不可预知的更新行为。

## <a name="see-also"></a>请参阅
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [如何：自动递增ClickOnce发布版本](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)