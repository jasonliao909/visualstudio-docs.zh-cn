---
title: 为 ClickOnce 应用指定“开始”菜单名称
description: 了解如何通过在“发布选项”对话框中设置产品名称来更改 ClickOnce 应用程序的显示名称。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665159"
---
# <a name="how-to-specify-a-start-menu-name-for-a-clickonce-application"></a>如何：指定 ClickOnce 应用程序的“开始”菜单名称
安装可供联机和脱机使用的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，将在“开始”菜单和“添加或删除程序”列表中添加一个条目 。 默认情况下，显示名称与应用程序程序集的名称相同，但可以通过在“发布选项”对话框中设置“产品名称”来更改显示名称 。

 “产品名称”将显示在 publish.htm 页面上；对于已安装的脱机应用程序，它是“开始”菜单中条目的名称，也是“添加或删除程序”中显示的名称 。

 “发布者名称”将出现在“产品名称”上方的 publish.htm 页面上，对于已安装的脱机应用程序，它也是包含“开始”菜单中应用程序图标的文件夹名称 。

 在 %appdata%\Microsoft\Windows\Start Menu\Programs\\<publisher name\> 中创建了“开始”菜单快捷方式或应用引用。 快捷方式或应用引用与产品名称同名。

 可在“项目设计器”的“发布”页上的“发布选项”对话框中设置“产品名称”和“发布者名称”属性    。

### <a name="to-specify-a-start-menu-name"></a>指定“开始”菜单名称

1. 在“解决方案资源管理器” 中选择了项目的情况下，在“项目”  菜单上单击“属性” 。

2. 单击 **“发布”** 选项卡。

3. 单击“选项”按钮以打开“发布选项”对话框 。

4. 单击“说明”。

5. 在“发布选项”对话框中，输入要在“产品名称”中显示的名称 。

6. 也可在“发布者名称”中输入发布者名称。

## <a name="see-also"></a>另请参阅
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)