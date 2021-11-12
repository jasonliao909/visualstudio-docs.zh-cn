---
title: 指定技术支持链接 | Microsoft Docs
description: 了解用于发布 ClickOnce 应用程序的“支持 URL”属性，该属性确定用户用于获取信息的网页或文件共享。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Support URL property
- product support, specifying URL for ClickOnce applications
- Web pages, ClickOnce
- Web sites, creating for ClickOnce support
- ClickOnce deployment, specifying support Web page address
- customer support, ClickOnce applications
- URLs, ClickOnce applications
ms.assetid: 500aebee-545e-4831-a78b-b8671a008015
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 03824a253bd2559d866ebd747f9257c300985219
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665868"
---
# <a name="how-to-specify-a-link-for-technical-support"></a>如何：指定技术支持链接
发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，“支持 URL”属性确定用户可以转至以获取应用程序相关信息的网页或文件共享。 此属性是可选的；如果提供了，该 URL 将显示在应用程序的条目“添加或删除程序”对话框中。

 可以在“项目设计器”的“发布”页上设置“支持 URL”属性  。

### <a name="to-specify-a-support-url"></a>指定支持 URL

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“选项”按钮以打开“发布选项”对话框 。

4. 单击“说明”。

5. 在“支持 URL”字段中，输入网站、网页或 UNC 共享的完全限定的路径。

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)