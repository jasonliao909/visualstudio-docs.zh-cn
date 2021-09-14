---
title: 设置 ClickOnce 发布版本 |Microsoft Docs
description: 了解如何设置 "ClickOnce 发布版本" 属性，该属性确定应用程序是否为更新。
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
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601007"
---
# <a name="how-to-set-the-clickonce-publish-version"></a>如何：设置 ClickOnce 发布版本
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `Publish Version` 属性确定你要发布的应用程序是否将被视为更新。 每次版本递增时，应用程序将作为更新发布。

 `Publish Version`可以在 **Project 设计器** 的 "**发布**" 页上设置属性。

> [!NOTE]
> 每次发布应用程序时，都有一个项目选项会自动递增 `Publish Version` 属性; 默认情况下启用此选项。 有关详细信息，请参阅[如何：自动递增 ClickOnce 发布版本](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)。

### <a name="to-change-the-publish-version"></a>更改发布版本

1. 在 **解决方案资源管理器** 中选择一个项目后，在 " **Project** " 菜单上单击 "**属性**"。

2. 单击 **“发布”** 选项卡。

3. 在 " **发布版本** " 字段中，递增 **主** 版本号、 **次** 版本号、 **内部** 版本号或 **修订** 版本的版本号。

    > [!NOTE]
    > 永远不应减小版本号;这样做可能会导致意外的更新行为。

## <a name="see-also"></a>另请参阅
- [选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)
- [如何：自动递增 ClickOnce 发布版本](../deployment/how-to-automatically-increment-the-clickonce-publish-version.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)