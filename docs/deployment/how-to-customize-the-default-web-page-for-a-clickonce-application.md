---
title: 自定义应用程序的默认ClickOnce页面
description: 了解将应用程序发布到 Web 时ClickOnce生成的网页，其中包含应用程序的名称和其他信息。
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
ms.openlocfilehash: 5185d3b49d8d1accaae7055f8bd073f9a25007dc92adff8c0978de957a55c284
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403953"
---
# <a name="how-to-customize-the-default-web-page-for-a-clickonce-application"></a>如何：自定义 ClickOnce 应用程序的默认网页
将应用程序ClickOnce Web 时，会自动生成一个网页，并随应用程序一起发布。 默认页包含应用程序的名称，以及用于安装应用程序、安装必备组件或在 MSDN 上访问帮助的链接。

> [!NOTE]
> 在页面上看到的实际链接取决于正在查看页面的计算机以及要包括的先决条件。

 网页的默认名称为 *Publish.htm;* 可以在设计器 中更改 **Project名称**。 有关详细信息，请参阅[如何：为应用程序指定发布ClickOnce页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)。

 只有在 *Publish.htm* 较新版本时，才发布该网页。

> [!NOTE]
> 对发布设置所做的更改不会影响Publish.htm页，但一个例外：如果在初始发布后添加或删除先决条件，先决条件列表将不再准确。 需要编辑先决条件链接的文本以反映更改。

### <a name="to-customize-the-publish-web-page"></a>自定义发布网页

1. 将ClickOnce应用程序发布到 Web 位置。 有关详细信息，请参阅[如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

2. 在 Web 服务器上，在Publish.htm或其他 HTML 编辑器中打开文件。

3. 根据需要自定义页面并保存。

4. 可选。 若要防止Visual Studio自定义发布网页，请取消选中"发布选项"对话框中每次发布后自动生成 **部署** 网页。

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [发布ClickOnce应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用应用程序安装ClickOnce先决条件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)
- [如何：为应用程序指定发布ClickOnce页](../deployment/how-to-specify-a-publish-page-for-a-clickonce-application.md)