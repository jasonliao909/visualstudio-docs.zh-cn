---
title: 指定文件复制位置|Microsoft Docs
description: 了解如何为应用程序设置"发布位置ClickOnce属性，该属性指定应用程序文件和清单的放入位置。
ms.custom:
- SEO-VS-2020
- seodec18
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
ms.openlocfilehash: 2425f428f5252c574eacb17c1c404bf06f80279e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122080437"
---
# <a name="how-to-specify-where-visual-studio-copies-the-files"></a>如何：指定 Visual Studio 复制文件的位置
使用 ClickOnce 发布应用程序时，“`Publish Location`”属性指定放置应用程序文件和清单的位置。 这可以是文件路径或 FTP 服务器的路径。

 可以在“项目设计器”的“发布”页上或使用发布向导指定 `Publish Location` 属性。 有关详细信息，请参阅[如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

> [!NOTE]
> 当使用 ClickOnce 安装多个版本的应用程序时，安装会将应用程序的早期版本移动到位于你指定的发布位置的名为“Archive”的文件夹中。 按照这种方式对早期版本进行存档，可以使安装目录与早期版本所在的文件夹分开。

### <a name="to-specify-a-publishing-location"></a>指定发布位置

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 在“发布位置”字段中，使用以下格式之一输入发布位置：

   - 若要发布到文件共享或磁盘路径，请通过使用 UNC 路径 (*\\ \Server\ApplicationName*) 或文件路径 (*C：\Deploy\ApplicationName*) 。

   - 若要发布到 FTP 服务器，请输入路径，格式为<em>ftp://ftp.microsoft.com/。 \<ApplicationName> </em>

     请注意，文本必须存在于"发布位置"框中，"浏览位置 **... (")** 按钮才能正常工作。

## <a name="see-also"></a>请参阅
- [发布ClickOnce应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布ClickOnce发布应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)