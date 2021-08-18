---
title: 指定 ClickOnce 应用 "开始"菜单名称
description: 了解如何通过在 "发布选项" 对话框中设置产品名称来更改 ClickOnce 应用程序的显示名称。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Start menu resource name
- Start menu name
- ClickOnce deployment, Start menu name
ms.assetid: 4b5183b2-2fd4-4433-9310-4a73bb12c4e3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 18e91e0bb0ebcb6a88d6f4c197cce9dfb4a04592
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051581"
---
# <a name="how-to-specify-a-start-menu-name-for-a-clickonce-application"></a>如何：指定 ClickOnce 应用程序的“开始”菜单名称
当 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序安装为联机和脱机使用时，会将一个条目添加到 " **开始** " 菜单和 " **添加或删除程序** " 列表中。 默认情况下，显示名称与应用程序程序集的名称相同，但您可以通过在 "**发布选项**" 对话框中设置 "**产品名称**" 来更改显示名称。

 **产品名称** 将显示在 " *publish.htm* " 页上;对于已安装的脱机应用程序，该应用程序将是 " **开始** " 菜单中条目的名称，并且还将是在 " **添加或删除程序**" 中显示的名称。

 **Publisher 名称** 将显示在 " *publish.htm* " 页上的 "**产品名称**" 中，对于已安装的脱机应用程序，它还将是包含 "**开始**" 菜单中的应用程序图标的文件夹的名称。

 "开始"菜单快捷方式或应用引用是在 *%appdata%\Microsoft\ Windows 启动 Menu\Programs \\<发布者名称 \>* 中创建的。 快捷方式或应用引用的名称与产品名称相同。

 可以在 "**发布选项**" 对话框中设置 "**产品名称**" 和 " **Publisher 名称**" 属性，该对话框可在 **Project 设计器** 的 "**发布**" 页中找到。

### <a name="to-specify-a-start-menu-name"></a>指定 "开始"菜单名称

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击 " **选项** " 按钮打开 " **发布选项** " 对话框。

4. 单击 " **说明**"。

5. 在 " **发布选项** " 对话框中，输入要在 " **产品名称**" 中显示的名称。

6. （可选）可以在 " **Publisher 名称**" 中输入发布者名称。

## <a name="see-also"></a>请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)