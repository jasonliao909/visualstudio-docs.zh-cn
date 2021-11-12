---
title: 指定发布页（ClickOnce 应用）
description: 了解如何为项目设置发布页属性，该属性可为 ClickOnce 应用程序指定一个网页。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications [ClickOnce], specifying publish page
- Publish Page property
- publishing, ClickOnce
- ClickOnce deployment, specifying publish page
ms.assetid: 9d70eebb-bdee-4b42-8e7e-7a07e199bdf7
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: cfc043fc62bc99a8e292d89c9217dcb80e53f781
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665867"
---
# <a name="how-to-specify-a-publish-page-for-a-clickonce-application"></a>如何：指定 ClickOnce 应用程序的发布页
发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，会生成一个默认网页 (publish.htm) 并随应用程序一起发布。 此页面包含应用程序的名称、指向安装应用程序和/或任何先决条件的链接以及指向介绍 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的帮助主题的链接。 项目的“发布页”属性可为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序指定网页名称。

 一旦指定了发布页面，下次发布时，该页将被复制到发布位置；如果再次发布，该页将不会被覆盖。 如果要自定义页面的外观，可以这样做，而不必担心会丢失所做的更改。 有关详细信息，请参阅[如何：自定义 ClickOnce 默认网页](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)。

 可在“项目设计器”的“发布”窗格中的“发布选项”对话框中设置“发布页”属性   。

### <a name="to-specify-a-custom-web-page-for-a-clickonce-application"></a>为 ClickOnce 应用程序指定自定义网页

1. 在“解决方案资源管理器” 中选择一个项目，然后在“项目”  菜单上单击“属性” 。

2. 选择“发布”窗格。

3. 单击“选项”按钮以打开“发布选项”对话框 。

4. 单击“部署”。

5. 在“发布选项”对话框中，确保选中了“发布后打开部署网页”复选框（默认情况下应选中） 。

6. 在“部署网页”框中，输入网页的名称，然后单击“确定” 。

### <a name="to-prevent-the-publish-page-from-launching-each-time-you-publish"></a>防止每次发布时都启动发布页

1. 在“解决方案资源管理器” 中选择一个项目，然后在“项目”  菜单上单击“属性” 。

2. 选择“发布”窗格。

3. 单击“选项”按钮以打开“发布选项”对话框 。

4. 单击“部署”。

5. 在“发布选项”对话框中，清除“发布后打开部署网页”复选框 。

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [如何：自定义 ClickOnce 的默认网页](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)