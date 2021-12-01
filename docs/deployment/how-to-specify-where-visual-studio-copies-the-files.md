---
title: 指定复制文件的位置 | Microsoft Docs
description: 了解如何设置 ClickOnce 应用程序的“发布位置”属性，该属性指定放置应用程序文件和清单的位置。
ms.custom:
- SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publishing, specifying location
- Publish Location property
ms.assetid: 6c552700-dda3-49fe-af98-4717344fda07
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: aa2e67f29c087b33a9614fab7b851de884034e9e
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129970875"
---
# <a name="how-to-specify-where-visual-studio-copies-the-files"></a>如何：指定 Visual Studio 复制文件的位置
使用 ClickOnce 发布应用程序时，“`Publish Location`”属性指定放置应用程序文件和清单的位置。 这可以是文件路径或 FTP 服务器的路径。

 可以在“项目设计器”的“发布”页上或使用发布向导指定 `Publish Location` 属性。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

> [!NOTE]
> 当使用 ClickOnce 安装多个版本的应用程序时，安装会将应用程序的早期版本移动到位于你指定的发布位置的名为“Archive”的文件夹中。 按照这种方式对早期版本进行存档，可以使安装目录与早期版本所在的文件夹分开。

### <a name="to-specify-a-publishing-location"></a>指定发布位置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在“发布位置”字段中，使用以下格式之一输入发布位置：

   - 若要发布到文件共享或磁盘路径，请使用 UNC 路径 (\\\\Server\ApplicationName) 或文件路径 (C:\Deploy\ApplicationName) 输入路径 。

   - 若要发布到 FTP 服务器，请使用格式 <em>ftp://ftp.microsoft.com/\<ApplicationName></em> 输入路径。

     请注意，“发布位置”框中必须存在文本才能使浏览（“...”）按钮正常工作 。

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)