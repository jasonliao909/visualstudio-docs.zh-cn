---
title: '指定应用应用的 (ClickOnce页) '
description: 了解如何为项目设置"发布页"属性，该属性允许你为应用程序ClickOnce网页。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122146311"
---
# <a name="how-to-specify-a-publish-page-for-a-clickonce-application"></a>如何：指定 ClickOnce 应用程序的发布页
发布应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 时，默认网页 (publish.htm) 应用程序一起生成和发布。 此页面包含应用程序的名称、用于安装应用程序和/或任何必备组件的链接，以及指向描述 的帮助主题的链接 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 项目的 **"** 发布页"属性允许为应用程序指定网页 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的名称。

 指定发布页后，下次发布时，该页将复制到发布位置;如果再次发布，将不会覆盖它。 如果要自定义页面的外观，可以这样做，而无需担心丢失更改。 有关详细信息，请参阅[如何：自定义ClickOnce默认网页](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)。

 可以在 **"发布** 选项"对话框中设置"发布页"属性，可从设计器 的"发布Project **访问**。

### <a name="to-specify-a-custom-web-page-for-a-clickonce-application"></a>为应用程序指定自定义ClickOnce页

1. 在 "属性"**中解决方案资源管理器**，在 Project菜单上单击 **"** 属性 **"。**

2. 选择" **发布"** 窗格。

3. 单击" **选项"** 按钮以打开" **发布选项"** 对话框。

4. 单击“部署”。

5. 在"**发布选项**"对话框中，确保选中"发布后打开部署网页"复选框 (默认情况下应选中) 。

6. 在 **"部署网页"** 框中，输入网页的名称，然后单击"确定 **"。**

### <a name="to-prevent-the-publish-page-from-launching-each-time-you-publish"></a>防止每次发布时启动发布页

1. 在 "属性"**中解决方案资源管理器**，在 Project菜单上单击 **"** 属性 **"。**

2. 选择" **发布"** 窗格。

3. 单击" **选项"** 按钮以打开" **发布选项"** 对话框。

4. 单击“部署”。

5. 在" **发布选项"** 对话框中，清除"发布后 **打开部署网页** "复选框。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
- [如何：自定义 ClickOnce 的默认网页](../deployment/how-to-customize-the-default-web-page-for-a-clickonce-application.md)