---
title: 更改 ClickOnce 应用程序的发布语言
description: 了解如何在 ClickOnce 中为本地化应用程序指定语言/区域性，而不是默认设置为开发计算机的语言/区域性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish language property
- ClickOnce deployment, changing publish language
- publishing, ClickOnce
ms.assetid: ef5024c4-cda1-4970-bc75-32a2a10c92c3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 4e34b5a28df05758eb24d6af2c907e99d0f9b9f7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665618"
---
# <a name="how-to-change-the-publish-language-for-a-clickonce-application"></a>如何：更改 ClickOnce 应用程序的发布语言

在发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，在安装过程中显示的用户界面默认为开发计算机的语言和区域性。 如果要发布本地化的应用程序，则需要指定与本地化版本匹配的语言和区域性。 这是由项目的 `Publish language` 属性决定的。

可在“项目设计器”的“发布”窗格中的“发布选项”对话框中设置 `Publish language` 属性  。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

## <a name="to-change-the-publish-language"></a>更改发布语言

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“选项”按钮以打开“发布选项”对话框 。

4. 单击“说明”。

5. 在“发布选项”对话框中，从“发布语言”下拉列表中选择语言和区域性，然后单击“确定”  。

## <a name="see-also"></a>另请参阅

- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)