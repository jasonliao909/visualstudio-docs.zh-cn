---
title: 自定义 ClickOnce 应用程序的默认网页
description: 了解将 ClickOnce 应用程序发布到 Web 时生成的网页，其中包含应用程序的名称和其他信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish.htm Web page
- ClickOnce deployment default Web page
- deploying applications [ClickOnce], publishing
- publishing, ClickOnce
ms.assetid: 418de18c-bee9-4f24-9cd9-0252d175070d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 2a1a3ae95889c3e57a2404090d7cf2db7a27e9a9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665610"
---
# <a name="how-to-customize-the-default-web-page-for-a-clickonce-application"></a>如何：自定义 ClickOnce 应用程序的默认网页
将 ClickOnce 应用程序发布到 Web 时，会自动生成一个网页并随应用程序一起发布。 默认页面包含应用程序的名称，以及指向安装应用程序、安装必备组件或访问 MSDN 上的帮助的链接。

> [!NOTE]
> 你在该页面上看到的实际链接取决于查看该页的计算机以及所包含的先决条件。

 网页的默认名称为“Publish.htm”；你可以在“项目设计器”中更改该名称。 有关详细信息，请参阅[如何：指定 ClickOnce 应用程序的发布页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)。

 只有在检测到较新版本时，才会发布 Publish.htm 网页。

> [!NOTE]
> 对“发布”设置所做的更改不会影响 Publish.htm 页，但有一种情况例外：如果在最初发布后添加或删除先决条件，则先决条件的列表将不再是准确的。 需要编辑先决条件链接的文本以反映所做的更改。

### <a name="to-customize-the-publish-web-page"></a>自定义发布网页

1. 将 ClickOnce 应用程序发布到一个 Web 位置。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

2. 在 Web 服务器上，在 Visual Web 设计器或其他 HTML 编辑器中打开“Publish.htm”文件。

3. 根据需要自定义页面并将其保存。

4. 可选。 若要防止 Visual Studio 覆盖自定义发布网页，请取消选中“发布选项”对话框中的“每次发布后自动生成部署网页”。

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：与 ClickOnce 应用程序一起安装系统必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [如何：指定 ClickOnce 应用程序的发布页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)